# EditorID

## Syntax

```pascal
function EditorID(ARecord: IwbMainRecord): string;
```

## Description

Returns the Editor ID of the record as a string.

This function retrieves the EditorID property, which provides direct access to the record's unique identifier string from the EDID subrecord. Editor IDs are human-readable names used for identifying records (e.g., "ArmorIronCuirass"). Returns an empty string if the record is invalid or has no EDID subrecord. More efficient than using ElementByPath to access the EDID element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the Editor ID from |

## Returns

Returns the Editor ID of the record as a string.

## Example

```pascal
sEditorID := EditorID(e);
if Assigned(sEditorID) then
	AddMessage(sEditorID);
```

## See Also

- [SetEditorID](IwbMainRecord_SetEditorID.md)
- [FormID](IwbMainRecord_FormID.md)
- [Signature](IwbMainRecord_Signature.md)
- [BaseRecordID](IwbMainRecord_BaseRecordID.md)
- [Name](IwbElement_Name.md)


