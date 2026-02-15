# GetPosition

## Syntax

```pascal
function GetPosition(ARecord: IwbMainRecord): TwbVector;
```

## Description

Returns the positional vector for `ARecord` when the record is a reference

The `x`, `y`, and `z` members of the return type can be accessed as [Single](http:__docwiki.embarcadero.com_Libraries_Rio_en_System.Single.md) fields.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The reference record to get the position from |

## Returns

Returns a TwbVector containing the X, Y, and Z coordinates.

## Example

```pascal
// Example 1: Display reference position coordinates
var
  pos: TwbVector;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    pos := GetPosition(e);
    AddMessage(Format('%s position:', [Name(e)]));
    AddMessage(Format('  X: %f', [pos.x]));
    AddMessage(Format('  Y: %f', [pos.y]));
    AddMessage(Format('  Z: %f', [pos.z]));
  end;
end;

// Example 2: Calculate distance between two references
var
  ref2: IwbMainRecord;
  pos1, pos2: TwbVector;
  dx, dy, dz, distance: Single;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    // Get second reference somehow...
    // ref2 := ...;

    if Assigned(ref2) and (Signature(ref2) = 'REFR') then begin
      pos1 := GetPosition(e);
      pos2 := GetPosition(ref2);

      dx := pos2.x - pos1.x;
      dy := pos2.y - pos1.y;
      dz := pos2.z - pos1.z;

      distance := Sqrt(dx*dx + dy*dy + dz*dz);
      AddMessage(Format('Distance between references: %f units', [distance]));
    end;
  end;
end;

// Example 3: Find references within area
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  centerPos, refPos: TwbVector;
  i, j, k, foundCount: integer;
  dx, dy, distance: Single;
  radius: Single;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    centerPos.x := 0.0;
    centerPos.y := 0.0;
    centerPos.z := 0.0;
    radius := 1000.0;

    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      foundCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) then begin
                  refPos := GetPosition(refRec);
                  dx := refPos.x - centerPos.x;
                  dy := refPos.y - centerPos.y;
                  distance := Sqrt(dx*dx + dy*dy);

                  if distance <= radius then begin
                    Inc(foundCount);
                    AddMessage(Format('  %s at distance %f', [Name(refRec), distance]));
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Found %d references within %f units', [foundCount, radius]));
    end;
  end;
end;

// Example 4: Adjust reference height (Z coordinate)
var
  pos: TwbVector;
  newZ: Single;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    pos := GetPosition(e);
    newZ := pos.z + 100.0; // Raise 100 units

    SetElementEditValue(e, 'DATA\Position\Z', FloatToStr(newZ));
    AddMessage(Format('%s raised from Z=%f to Z=%f',
      [Name(e), pos.z, newZ]));
  end;
end;
```

## See Also

- [GetRotation](IwbMainRecord_GetRotation.md)


