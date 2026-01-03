# FormID

## Syntax

```pascal
function FormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the Form ID of `ARecord`

**Note:** The Form ID returned by this function is not relative to file load order.

## Example

```pascal
if FormID(e) and $00FFFFFF = 0 then
	AddMessage(FullPath(e));
```

## See Also

- [CompareExchangeFormID](IwbMainRecord_CompareExchangeFormID.md)
- [FileFormIDtoLoadOrderFormID](../IwbFile/IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [GetNewFormID](../IwbFile/IwbFile_GetNewFormID.md)
- [LoadOrderFormIDtoFileFormID](../IwbFile/IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](../IwbFile/IwbFile_RecordByFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
