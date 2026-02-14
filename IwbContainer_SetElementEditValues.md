# SetElementEditValues

## Syntax

```pascal
procedure SetElementEditValues(AContainer: IwbContainer; APath: string; AValue: string);
```

## Description

Changes the edit value of an element in the container identified by the specified path.

This procedure modifies the human-readable edit value of an element. The path parameter uses slash notation to navigate to nested elements. The value is converted from string to the appropriate type for the target element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container containing the element to modify |
| APath | string | The element path to the value |
| AValue | string | The new edit value to set |

## Example

```pascal
var
  container: IwbContainer;
begin
  SetElementEditValues(container, 'EDID', 'NewEditorID');
end
```

## See Also

- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)
- [SetEditValue](IwbElement_SetEditValue.md)


