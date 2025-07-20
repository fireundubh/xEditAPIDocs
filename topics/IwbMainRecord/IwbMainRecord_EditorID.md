# EditorID

## Syntax

```pascal
function EditorID(ARecord: IwbMainRecord): string;
```

## Description

Returns the edit value of the `EDID` element of `ARecord`

## Example

```pascal
sEditorID := EditorID(e);
if Assigned(sEditorID) then
	AddMessage(sEditorID);
```

## See Also

- [BaseRecordID](IwbMainRecord_BaseRecordID.md)
- [GetFileName](IwbFile_GetFileName.md)
- [Name](IwbElement_Name.md)
- [SetEditorID](IwbMainRecord_SetEditorID.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [ShortName](IwbElement_ShortName.md)
- [Signature](IwbMainRecord_Signature.md)
