# GetEditValue

## Syntax

```pascal
function GetEditValue(AElement: IwbElement): string;
```

## Description

Returns a string representation of the element's value.

This function provides the editable value of an element as a string, which is useful for displaying or modifying element values through user interfaces.

## Example

```pascal
var
  element: IwbElement;
  value: string;
begin
  value := GetEditValue(element);
  // Use the string value
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)
- [GetElementEditValues](../IwbContainer/IwbContainer_GetElementEditValues.md)
- [SetElementEditValues](../IwbContainer/IwbContainer_SetElementEditValues.md)
