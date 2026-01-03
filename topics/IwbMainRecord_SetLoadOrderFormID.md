# SetLoadOrderFormID

## Syntax

```pascal
procedure SetLoadOrderFormID(ARecord: IwbMainRecord; ALoadOrderFormID: Cardinal);
```

## Description

Changes the Form ID of `ARecord` to `ALoadOrderFormID`

If the load order Form ID of an overriding record is changed to a Form ID with a load order prefix inside the containing file, that record will become a new record.

If the load order Form ID of any record is changed to a Form ID with a load order prefix outside the containing file, that record will become an injected record.

An exception will be raised when one of the following conditions is met:

- when `ALoadOrderFormID` refers to an existing Form ID; or 
- when `ALoadOrderFormID` refers to a Form ID that cannot be mapped to a master file.

## Example

```pascal
SetLoadOrderFormID(e, $060FFFFF);
AddMessage(IntToHex(GetLoadOrderFormID(e), 8));  // Output: 060FFFFF
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)


