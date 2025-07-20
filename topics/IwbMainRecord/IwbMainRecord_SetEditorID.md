# SetEditorID

## Syntax

```pascal
procedure SetEditorID(ARecord: IwbMainRecord; AEditorID: string);
```

## Description

Changes the native value of the `EditorID` property of `ARecord` to `AEditorID`

The `EditorID` property corresponds to the `EDID` element.

## Example

```pascal
sEditorID := EditorID(e);
if not SameText(sEditorID, 'NewID') then 
	SetEditorID(e, 'NewID');
```

## See Also

- [EditorID - IwbMainRecord](IwbMainRecord_EditorID.md)
- [SetEditValue - IwbElement](IwbElement_SetEditValue.md)
- [SetElementEditValues - IwbContianer](IwbContainer_SetElementEditValues.md)
