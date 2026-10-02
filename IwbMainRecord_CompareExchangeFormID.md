# CompareExchangeFormID

## Syntax

```pascal
function CompareExchangeFormID(ARecord: IwbMainRecord; AOldFormID: Cardinal; ANewFormID: Cardinal): Boolean;
```

## Description

Rewrites FormID values stored inside `ARecord`. Each contained FormID that currently refers to `AOldFormID` is changed to `ANewFormID`. Both arguments are load-order FormIDs, the same kind [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md) returns, not file FormIDs. This does not change `ARecord`'s own FormID; use [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md) for that.

Returns `True` if at least one contained FormID changed, and `False` if `ARecord` is a main record and none matched.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record whose contained FormIDs are rewritten |
| AOldFormID | Cardinal | Load-order FormID to find inside `ARecord` |
| ANewFormID | Cardinal | Load-order FormID to write in its place |

## Returns

Returns `True` if at least one contained FormID changed, `False` if `ARecord` is a main record and none matched.

## Example

```pascal
// Example 1: Update all references after changing record FormID
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
  i, refCount: integer;
  success: boolean;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newFormID := FileFormIDtoLoadOrderFormID(GetFile(e), GetNewFormID(GetFile(e)));

    refCount := ReferencedByCount(e);
    AddMessage(Format('Updating %d references from %s to %s',
      [refCount, IntToHex(oldFormID, 8), IntToHex(newFormID, 8)]));

    for i := 0 to refCount - 1 do begin
      refByRec := ReferencedByIndex(e, i);
      if Assigned(refByRec) then begin
        success := CompareExchangeFormID(refByRec, oldFormID, newFormID);
        if success then
          AddMessage(Format('  Updated: %s', [EditorID(refByRec)]))
        else
          AddMessage(Format('  FAILED: %s', [EditorID(refByRec)]));
      end;
    end;

    SetLoadOrderFormID(e, newFormID);
  end;
end;

// Example 2: Replace one load-order FormID stored inside the record
var
  oldFormID, newFormID: Cardinal;
  success: boolean;
begin
  if Assigned(e) then begin
    oldFormID := $01ABC123;
    newFormID := $02ABC123;

    success := CompareExchangeFormID(e, oldFormID, newFormID);
    if success then
      AddMessage('Updated a contained FormID')
    else
      AddMessage('No contained FormID matched');
  end;
end;

// Example 3: Batch update FormIDs when changing load order
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newFormID := FileFormIDtoLoadOrderFormID(GetFile(e), GetNewFormID(GetFile(e)));

    // Stop if a referencing record does not contain the old FormID.
    while ReferencedByCount(e) > 0 do begin
      refByRec := ReferencedByIndex(e, 0);
      if not Assigned(refByRec) then
        Break;
      if not CompareExchangeFormID(refByRec, oldFormID, newFormID) then
        Break;
    end;

    SetLoadOrderFormID(e, newFormID);
  end;
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)


