# GetEditValue

## Syntax

```pascal
function GetEditValue(AElement: IwbElement): string;
```

## Description

Returns the element's value as a human-readable and editable string representation.

This function retrieves the EditValue property, which provides a formatted string suitable for display and editing in user interfaces. The format depends on the element's definition type (e.g., integers as decimal strings, FormIDs as hex strings, enums as their names). Returns an empty string if the element is invalid.

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
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetValue](IwbElement_GetValue.md)
- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)


