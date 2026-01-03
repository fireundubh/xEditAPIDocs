# SetElementEditValues

## Syntax

```pascal
procedure SetElementEditValues(AContainer: IwbContainer; APath: string; AValue: string);
```

## Description

Changes the edit value of an element in the container identified by the specified path.

This procedure modifies the human-readable edit value of an element. The path parameter uses slash notation to navigate to nested elements. The value is converted from string to the appropriate type for the target element.

## Examples

```pascal
var
  container: IwbContainer;
begin
  SetElementEditValues(container, 'EDID', 'NewEditorID');
end
```

## See Also

- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)


