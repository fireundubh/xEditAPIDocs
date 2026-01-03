# GetLoadOrderFormID

## Syntax

```pascal
function GetLoadOrderFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the Form ID of `ARecord` relative to the current load order

`FixedFormID`, `FormID`, and `GetLoadOrderFormID` will return different Form ID values when `ARecord` is overridden but not when `ARecord` is the overriding record.


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

- [FileFormIDtoLoadOrderFormID](../IwbFile/IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [LoadOrderFormIDtoFileFormID](../IwbFile/IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](../IwbFile/IwbFile_RecordByFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
