# SetLoadOrderFormID

## Syntax

```pascal
procedure SetLoadOrderFormID(ARecord: IwbMainRecord; ALoadOrderFormID: Cardinal);
```

## Description

Changes the record's FormID to a new value specified in load order format.

`ALoadOrderFormID` is a load-order FormID, not the file-local value accepted by [RecordByFormID](IwbFile_RecordByFormID.md). The call converts it to the file's FormID before storing. On Morrowind the call does nothing. The file header's FormID is cleared instead of taking `ALoadOrderFormID`.

Changing an override's FormID onto the current file makes it a new record in that file. A FormID that belongs to another file becomes an override when that record already exists, and is injected when it does not. Raises an exception if that FormID is already used in the file, or if the object ID is below `$800`, is not a hardcoded ID, and the file has no master that can own it.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to change the Form ID on |
| ALoadOrderFormID | Cardinal | The new load order Form ID to assign |

## Returns

Returns nothing.

## Example

```pascal
// Example 1: Assign new FormID to copied record
var
  copiedRec: IwbMainRecord;
  targetFile: IwbFile;
  newFormID: Cardinal;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(0);
    if Assigned(targetFile) then begin
      copiedRec := wbCopyElementToFile(e, targetFile, false, true);
      if Assigned(copiedRec) then begin
        newFormID := GetNewFormID(targetFile);
        SetLoadOrderFormID(copiedRec, newFormID);
        AddMessage(Format('Assigned new FormID: %s', [IntToHex(newFormID, 8)]));
      end;
    end;
  end;
end;

// Example 2: Change FormID file index to current plugin
var
  currentFile: IwbFile;
  currentFormID, newFormID: Cardinal;
  loadOrder: byte;
begin
  if Assigned(e) then begin
    currentFile := GetFile(e);
    if Assigned(currentFile) then begin
      currentFormID := GetLoadOrderFormID(e);
      loadOrder := GetLoadOrder(currentFile);
      newFormID := (currentFormID and $00FFFFFF) or (loadOrder shl 24);

      SetLoadOrderFormID(e, newFormID);
      AddMessage(Format('Changed FormID from %s to %s',
        [IntToHex(currentFormID, 8), IntToHex(newFormID, 8)]));
    end;
  end;
end;

// Example 3: Update all references after changing FormID
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
  i, refCount: integer;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newFormID := GetNewFormID(GetFile(e));

    // Update all records that reference this one
    refCount := ReferencedByCount(e);
    for i := 0 to refCount - 1 do begin
      refByRec := ReferencedByIndex(e, i);
      if Assigned(refByRec) then
        CompareExchangeFormID(refByRec, oldFormID, newFormID);
    end;

    // Now change the record's FormID
    SetLoadOrderFormID(e, newFormID);
    AddMessage(Format('Updated FormID and %d references', [refCount]));
  end;
end;
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)


