# FormID

## Syntax

```pascal
function FormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the record's FormID as it appears in the file (file-local FormID).

This function retrieves the FormID property and converts it to a Cardinal. The returned value is the file-local FormID, which includes the file index in the upper byte (load order position at the time the file was saved). This is NOT the same as the current load order FormID. For runtime load order FormIDs, use GetLoadOrderFormID instead. Returns 0 for invalid records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the Form ID from |

## Returns

Returns the Form ID as a Cardinal value (not relative to load order).

## Example

```pascal
// Example 1: Get file-local FormID
var
  formID: Cardinal;
begin
  if Assigned(e) then begin
    formID := FormID(e);
    AddMessage(Format('File-local FormID: %s', [IntToHex(formID, 8)]));
  end;
end;

// Example 2: Check if FormID is from master file (object ID only)
var
  formID, objectID: Cardinal;
begin
  if Assigned(e) then begin
    formID := FormID(e);
    objectID := formID and $00FFFFFF; // Strip file index byte

    if objectID = 0 then
      AddMessage('ERROR: Invalid object ID: ' + FullPath(e))
    else
      AddMessage(Format('Object ID: %s', [IntToHex(objectID, 6)]));
  end;
end;

// Example 3: Compare file FormID with load order FormID
var
  fileFormID, loadOrderFormID: Cardinal;
  fileIndex, loadOrderIndex: byte;
begin
  if Assigned(e) then begin
    fileFormID := FormID(e);
    loadOrderFormID := GetLoadOrderFormID(e);

    fileIndex := fileFormID shr 24;
    loadOrderIndex := loadOrderFormID shr 24;

    AddMessage(Format('File FormID: %s (file index: %d)', [IntToHex(fileFormID, 8), fileIndex]));
    AddMessage(Format('Load Order FormID: %s (LO index: %d)', [IntToHex(loadOrderFormID, 8), loadOrderIndex]));

    if fileIndex <> loadOrderIndex then
      AddMessage('WARNING: File index differs from current load order position');
  end;
end;
```

## See Also

- [CompareExchangeFormID](IwbMainRecord_CompareExchangeFormID.md)
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [GetNewFormID](IwbFile_GetNewFormID.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


