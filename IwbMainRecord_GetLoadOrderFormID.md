# GetLoadOrderFormID

## Syntax

```pascal
function GetLoadOrderFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the FormID adjusted for the current runtime load order.

This function retrieves the LoadOrderFormID property and converts it to a Cardinal. The returned value has the file index updated to reflect the current load order position (not the saved file index). This is the FormID the game engine uses at runtime. Returns 0 for invalid records. Use this when you need the FormID that will actually work in the game, especially when load order has changed since the file was saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the load order Form ID from |

## Returns

Returns the Form ID relative to the current load order as a Cardinal value.

## Example

With `Unofficial Fallout 4 Patch.esp` loaded and `[MISC:06022DC0]` selected in `DLCNukaWorld.esm`:

```pascal
sFixedFormID     := IntToHex(FixedFormID(e),        8);
sFormID          := IntToHex(FormID(e),             8);
sLoadOrderFormID := IntToHex(GetLoadOrderFormID(e), 8);

AddMessage(sFixedFormID);      // Output: 01022DC0
AddMessage(sFormID);           // Output: 01022DC0
AddMessage(sLoadOrderFormID);  // Output: 06022DC0
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


