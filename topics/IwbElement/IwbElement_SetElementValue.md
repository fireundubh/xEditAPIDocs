# SetEditValue

## Syntax

```pascal
function SetEditValue(AElement: IwbElement; AValue: string): boolean;
```

## Description

Sets the element's value using a string representation.

This function attempts to set the element's value using a string representation. Returns true if the value was successfully set, false otherwise. The string format must be appropriate for the element type.

## Example

```pascal
var
    element: IwbElement;
    success: boolean;
begin
    success := SetEditValue(element, '100');
    if success then
        // Value was successfully set
end;
```

## See Also

- [GetEditValue - IwbElement](IwbElement_GetEditValue.md)
- [SetNativeValue - IwbElement](IwbElement_SetNativeValue.md)
