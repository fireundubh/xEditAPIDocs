# GetValue

## Syntax

```pascal
function GetValue(AElement: IwbElement): string;
```

## Description

Returns the string display value of an element as it is displayed in the UI. This provides the formatted, human-readable representation of the element's value, useful for things like decoded texture hashes, localized strings, and other display-specific formatting.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose display value to retrieve |

## Returns

Returns a string containing the formatted display value of the element as it appears in the xEdit UI.

## Example

```pascal
var
  element: IwbElement;
  displayValue: string;
begin
  element := ElementByPath(e, 'EDID');
  displayValue := GetValue(element);
  AddMessage('Editor ID display value: ' + displayValue);
end;
```

## See Also

- [GetEditValue](IwbElement_GetEditValue.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [GetElementValues](IwbContainer_GetElementValues.md)


