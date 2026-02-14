# SetLoadOrderFormID

## Syntax

```pascal
procedure SetLoadOrderFormID(ARecord: IwbMainRecord; ALoadOrderFormID: Cardinal);
```

## Description

Changes the record's FormID to a new value specified in load order format.

This function assigns to the LoadOrderFormID property, converting the load order FormID to file-local format before storing. The upper byte of the FormID determines the owning file. Changing an override's FormID to use the current file's index converts it to a new master record. Changing any record's FormID to use another file's index makes it an injected record. Raises an exception if the new FormID already exists or cannot be mapped to a valid master.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to change the Form ID on |
| ALoadOrderFormID | Cardinal | The new load order Form ID to assign |

## Example

```pascal
SetLoadOrderFormID(e, $060FFFFF);
AddMessage(IntToHex(GetLoadOrderFormID(e), 8));  // Output: 060FFFFF
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)


