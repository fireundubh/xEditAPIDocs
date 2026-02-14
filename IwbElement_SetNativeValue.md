# SetNativeValue

## Syntax

```pascal
procedure SetNativeValue(AElement: IwbElement; AValue: Variant);
```

## Description

Sets the element's value directly using its native data type.

This function assigns to the NativeValue property, which accepts a Variant containing the value in the appropriate type (integer, float, string, etc.). No string parsing or conversion is performed. The element must be editable and the Variant type must be compatible with the element's definition. This is more efficient than SetEditValue when you already have the value in its native type.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to set the value for |
| AValue | Variant | The new value in its native data type |

## Returns

This procedure does not return a value.

## Example

```pascal
var
    element: IwbElement;
    success: boolean;
begin
    success := SetNativeValue(element, 100); // Set integer value
    if success then
        // Value was successfully set
end;
```

## See Also

- [GetNativeValue](IwbElement_GetNativeValue.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [GetEditValue](IwbElement_GetEditValue.md)
- [SetElementNativeValues](IwbContainer_SetElementNativeValues.md)


