# GetNativeValue

## Syntax

```pascal
function GetNativeValue(AElement: IwbElement): Variant;
```

## Description

Returns the element's value in its native type.

This function returns the element's value as a Variant containing the native data type (integer, float, string, etc.) rather than a string representation. This is useful when you need to perform calculations or comparisons with the actual value.

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


