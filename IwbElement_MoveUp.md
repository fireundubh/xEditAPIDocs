# MoveUp

## Syntax

```pascal
procedure MoveUp(AElement: IwbElement);
```

## Description

Moves the element up one position (toward a lower index) within its parent container.

This function calls the element's MoveUp method, which swaps the element with the previous element in the container. Only works for elements in arrays or sorted containers. The element must not already be at the first position. Use CanMoveUp first to verify the operation is valid, otherwise the method may have no effect or raise an exception.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to move up in its array |

## Example

```pascal
var
    element: IwbElement;
begin
    if CanMoveUp(element) then
        MoveUp(element);
end;
```

## See Also

- [CanMoveUp](IwbElement_CanMoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)
- [CanMoveDown](IwbElement_CanMoveDown.md)


