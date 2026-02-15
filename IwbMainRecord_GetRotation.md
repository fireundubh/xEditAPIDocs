# GetRotation

## Syntax

```pascal
function GetRotation(ARecord: IwbMainRecord): TwbVector;
```

## Description

Returns the rotational vector for `ARecord` when the record is a reference

The `x`, `y`, and `z` members of the return type can be accessed as [Single](http:__docwiki.embarcadero.com_Libraries_Rio_en_System.Single.md) fields.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The reference record to get the rotation from |

## Returns

Returns a TwbVector containing the X, Y, and Z rotation values.

## Example

```pascal
// Example 1: Display reference rotation angles
var
  rot: TwbVector;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    rot := GetRotation(e);
    AddMessage(Format('%s rotation:', [Name(e)]));
    AddMessage(Format('  X (Pitch): %f degrees', [rot.x * 180 / Pi]));
    AddMessage(Format('  Y (Roll):  %f degrees', [rot.y * 180 / Pi]));
    AddMessage(Format('  Z (Yaw):   %f degrees', [rot.z * 180 / Pi]));
  end;
end;

// Example 2: Check if reference is upright
var
  rot: TwbVector;
  pitchDeg, rollDeg: Single;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    rot := GetRotation(e);

    // Convert radians to degrees
    pitchDeg := rot.x * 180 / Pi;
    rollDeg := rot.y * 180 / Pi;

    if (Abs(pitchDeg) < 5) and (Abs(rollDeg) < 5) then
      AddMessage(Format('%s is upright', [Name(e)]))
    else
      AddMessage(Format('%s is tilted (pitch=%f, roll=%f)',
        [Name(e), pitchDeg, rollDeg]));
  end;
end;

// Example 3: Find references facing specific direction
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  rot: TwbVector;
  i, j, k, foundCount: integer;
  yawDeg: Single;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      foundCount := 0;

      AddMessage('Finding references facing north (yaw ~0)...');

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) then begin
                  rot := GetRotation(refRec);
                  yawDeg := rot.z * 180 / Pi;

                  // Check if facing north (within 10 degrees)
                  if Abs(yawDeg) < 10 then begin
                    Inc(foundCount);
                    AddMessage(Format('  %s (yaw=%f)', [Name(refRec), yawDeg]));
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Found %d north-facing references', [foundCount]));
    end;
  end;
end;

// Example 4: Rotate reference to face specific direction
var
  rot: TwbVector;
  newYaw: Single;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    rot := GetRotation(e);

    // Rotate 90 degrees clockwise (add Pi/2 radians)
    newYaw := rot.z + (Pi / 2);

    // Normalize to -Pi to Pi range
    while newYaw > Pi do
      newYaw := newYaw - 2*Pi;
    while newYaw < -Pi do
      newYaw := newYaw + 2*Pi;

    SetElementEditValue(e, 'DATA\Rotation\Z', FloatToStr(newYaw));
    AddMessage(Format('%s rotated from %f to %f degrees',
      [Name(e), rot.z * 180 / Pi, newYaw * 180 / Pi]));
  end;
end;
```

## See Also

- [GetPosition](IwbMainRecord_GetPosition.md)


