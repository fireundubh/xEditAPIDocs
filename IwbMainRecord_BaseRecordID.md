# BaseRecordID

## Syntax

```pascal
function BaseRecordID(AReference: IwbMainRecord): Cardinal;
```

## Description

Returns the load order Form ID of the main record linked to the `NAME` subrecord for `AReference`

**Note:** `AReference` must be a main record with the signature `ACHR` (Placed NPC) or `REFR` (Placed Object).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AReference | IwbMainRecord | The reference record (ACHR or REFR) to get the base record ID from |

## Returns

Returns the load order Form ID of the base record as a Cardinal value.

## Example

```pascal
// Example 1: Get FormID of base object
var
  baseFormID: Cardinal;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    baseFormID := BaseRecordID(e);
    if baseFormID <> 0 then
      AddMessage(Format('%s has base FormID: %s',
        [Name(e), IntToHex(baseFormID, 8)]))
    else
      AddMessage(Format('%s has no base record', [Name(e)]));
  end;
end;

// Example 2: Check if reference uses specific base FormID
var
  baseFormID, targetFormID: Cardinal;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    targetFormID := $0010A8A6; // Example FormID to check
    baseFormID := BaseRecordID(e);

    if baseFormID = targetFormID then
      AddMessage(Format('%s uses target base object', [Name(e)]))
    else
      AddMessage(Format('%s uses different base: %s',
        [Name(e), IntToHex(baseFormID, 8)]));
  end;
end;

// Example 3: Group references by base FormID
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, idx: integer;
  baseFormID: Cardinal;
  baseFormIDs: TStringList;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      baseFormIDs := TStringList.Create;
      try
        for i := 0 to Pred(ElementCount(childGroup)) do begin
          blockGroup := ElementByIndex(childGroup, i);
          if Assigned(blockGroup) then begin
            for j := 0 to Pred(ElementCount(blockGroup)) do begin
              subBlock := ElementByIndex(blockGroup, j);
              if Assigned(subBlock) then begin
                for k := 0 to Pred(ElementCount(subBlock)) do begin
                  refRec := ElementByIndex(subBlock, k);
                  if Assigned(refRec) and (Signature(refRec) = 'REFR') then begin
                    baseFormID := BaseRecordID(refRec);
                    if baseFormID <> 0 then begin
                      idx := baseFormIDs.IndexOf(IntToHex(baseFormID, 8));
                      if idx >= 0 then
                        baseFormIDs.Objects[idx] := TObject(Integer(baseFormIDs.Objects[idx]) + 1)
                      else
                        baseFormIDs.AddObject(IntToHex(baseFormID, 8), TObject(1));
                    end;
                  end;
                end;
              end;
            end;
          end;
        end;

        AddMessage(Format('Base objects used in %s:', [EditorID(e)]));
        for i := 0 to baseFormIDs.Count - 1 do
          AddMessage(Format('  %s: %d instance(s)',
            [baseFormIDs[i], Integer(baseFormIDs.Objects[i])]));
      finally
        baseFormIDs.Free;
      end;
    end;
  end;
end;

// Example 4: Find reference by base FormID
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k: integer;
  targetFormID, baseFormID: Cardinal;
  found: boolean;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    targetFormID := $0010A8A6; // FormID to find
    found := false;

    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and (Signature(refRec) = 'REFR') then begin
                  baseFormID := BaseRecordID(refRec);
                  if baseFormID = targetFormID then begin
                    AddMessage(Format('Found: %s', [Name(refRec)]));
                    found := true;
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      if not found then
        AddMessage(Format('No instances of FormID %s found', [IntToHex(targetFormID, 8)]));
    end;
  end;
end;
```

## See Also

- [BaseRecord](IwbMainRecord_BaseRecord.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


