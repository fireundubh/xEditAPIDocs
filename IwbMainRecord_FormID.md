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
if FormID(e) and $00FFFFFF = 0 then
	AddMessage(FullPath(e));
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


