# GetEditValue

## Syntax

```pascal
function GetEditValue(AElement: IwbElement): string;
```

## Description

Returns a string representation of the element's value.

This function provides the editable value of an element as a string, which is useful for displaying or modifying element values through user interfaces.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the edit value from |

## Returns

Returns the element's edit value as a string.

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
- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)


