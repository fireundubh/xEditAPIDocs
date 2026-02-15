# BaseRecord

## Syntax

```pascal
function BaseRecord(AReference: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the main record linked to the `NAME` subrecord for `AReference`

**Note:** `AReference` must be a main record with the signature `ACHR` (Placed NPC) or `REFR` (Placed Object).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AReference | IwbMainRecord | The reference record (ACHR or REFR) to get the base record from |

## Returns

Returns the IwbMainRecord linked to the NAME subrecord of the reference.

## Example

```pascal
// Example 1: Get base object of placed reference
var
  baseRec: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    baseRec := BaseRecord(e);
    if Assigned(baseRec) then
      AddMessage(Format('%s is an instance of %s (%s)',
        [Name(e), EditorID(baseRec), Signature(baseRec)]))
    else
      AddMessage(Format('%s has no base record', [Name(e)]));
  end;
end;

// Example 2: Filter placed references by base object type
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec, baseRec: IwbMainRecord;
  i, j, k, doorCount: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      doorCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and (Signature(refRec) = 'REFR') then begin
                  baseRec := BaseRecord(refRec);
                  if Assigned(baseRec) and (Signature(baseRec) = 'DOOR') then begin
                    Inc(doorCount);
                    AddMessage(Format('  Door: %s', [Name(refRec)]));
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Found %d door(s) in %s', [doorCount, EditorID(e)]));
    end;
  end;
end;

// Example 3: Copy base object properties to reference
var
  baseRec: IwbMainRecord;
  baseName: string;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    baseRec := BaseRecord(e);
    if Assigned(baseRec) then begin
      baseName := GetElementEditValue(baseRec, 'FULL');
      if baseName <> '' then begin
        AddMessage(Format('Base object name: %s', [baseName]));
        AddMessage(Format('Base object type: %s', [Signature(baseRec)]));
        AddMessage(Format('Base object EditorID: %s', [EditorID(baseRec)]));
      end;
    end;
  end;
end;

// Example 4: Find all placed instances of specific base object
var
  refRec: IwbMainRecord;
  i, count, instanceCount: integer;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    instanceCount := 0;

    AddMessage(Format('Finding placed instances of %s...', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      refRec := ReferencedByIndex(e, i);
      if Assigned(refRec) then begin
        sig := Signature(refRec);
        if (sig = 'REFR') or (sig = 'ACHR') then begin
          // Verify this is actually the base record
          if BaseRecord(refRec) = e then begin
            Inc(instanceCount);
            AddMessage(Format('  Instance %d: %s', [instanceCount, Name(refRec)]));
          end;
        end;
      end;
    end;

    AddMessage(Format('Total instances: %d', [instanceCount]));
  end;
end;
```

## See Also

- [BaseRecordID](IwbMainRecord_BaseRecordID.md)


