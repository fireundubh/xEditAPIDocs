# SetEditorID

## Syntax

```pascal
procedure SetEditorID(ARecord: IwbMainRecord; AEditorID: string);
```

## Description

Sets the Editor ID of the record to the specified string value.

This function assigns to the EditorID property, which directly modifies the EDID subrecord's value. The EDID subrecord will be created if it doesn't exist. Editor IDs must be unique within a plugin for proper reference resolution. The record must be editable for this operation to succeed. More efficient than using SetElementEditValues to modify the EDID element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Editor ID on |
| AEditorID | string | The new Editor ID value to assign |

## Example

```pascal
sEditorID := EditorID(e);
if not SameText(sEditorID, 'NewID') then 
	SetEditorID(e, 'NewID');
```

## See Also

- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)
- [Signature](IwbMainRecord_Signature.md)


