# GetNativeValue

## Syntax

```pascal
function GetNativeValue(AElement: IwbElement): Variant;
```

## Description

Returns the element's value in its native data type as a Variant.

This function retrieves the NativeValue property, which returns the element's internal value without string formatting. The Variant type depends on the element definition (e.g., integers for numeric fields, floats for real numbers, strings for text). Returns an empty string (as Variant) if the element is invalid. Prefer this over GetEditValue for programmatic comparisons and calculations.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the native value from |

## Returns

Returns the element's native value as a Variant type.

## Example

```pascal
var
  element: IwbElement;
  value: Variant;
begin
  value := GetNativeValue(element);
  // Use the native value
  if VarType(value) = varInteger then
    // Handle integer value
end;
```

## See Also

- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetEditValue](IwbElement_GetEditValue.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [GetValue](IwbElement_GetValue.md)
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)


