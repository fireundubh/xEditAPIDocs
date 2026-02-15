# CompareExchangeFormID

## Syntax

```pascal
function CompareExchangeFormID(ARecord: IwbMainRecord; AOldFormID: TwbFormID; ANewFormID: TwbFormID): Boolean;
```

## Description

Attempts to change the Form ID of `ARecord` from `AOldFormID` to `ANewFormID`

Returns `True` if the attempt was successful and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to change the Form ID on |
| AOldFormID | TwbFormID | The expected current Form ID to compare against |
| ANewFormID | TwbFormID | The new Form ID to assign if the comparison matches |

## Returns

Returns `True` if the Form ID was successfully changed, `False` otherwise.

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
    newFormID := GetNewFormID(GetFile(e));

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

// Example 2: Thread-safe FormID update with verification
var
  currentFormID, expectedFormID, newFormID: Cardinal;
  success: boolean;
begin
  if Assigned(e) then begin
    expectedFormID := $01ABC123;
    newFormID := $02ABC123;

    currentFormID := GetLoadOrderFormID(e);
    if currentFormID = expectedFormID then begin
      success := CompareExchangeFormID(e, expectedFormID, newFormID);
      if success then
        AddMessage('FormID updated successfully')
      else
        AddMessage('FormID update failed - concurrent modification?');
    end else begin
      AddMessage(Format('ERROR: Expected FormID %s but found %s',
        [IntToHex(expectedFormID, 8), IntToHex(currentFormID, 8)]));
    end;
  end;
end;

// Example 3: Batch update FormIDs when changing load order
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
  newLoadOrder: byte;
  i: integer;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newLoadOrder := 10;
    newFormID := (oldFormID and $00FFFFFF) or (newLoadOrder shl 24);

    // Update all referencing records
    while ReferencedByCount(e) > 0 do begin
      refByRec := ReferencedByIndex(e, 0);
      if Assigned(refByRec) then
        CompareExchangeFormID(refByRec, oldFormID, newFormID);
    end;

    // Finally update the record itself
    SetLoadOrderFormID(e, newFormID);
    AddMessage(Format('Changed load order index from %d to %d',
      [oldFormID shr 24, newLoadOrder]));
  end;
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)


