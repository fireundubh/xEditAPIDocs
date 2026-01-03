# SetNativeValue

## Syntax

```pascal
function SetNativeValue(AElement: IwbElement; AValue: Variant): boolean;
```

## Description

Sets the element's value using its native data type.

This function attempts to set the element's value using a Variant containing the appropriate native data type. Returns `true` if the value was successfully set, `false` otherwise. This is more efficient than `SetEditValue` when working with native data types.

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
