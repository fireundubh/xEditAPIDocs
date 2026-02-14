# MoveDown

## Syntax

```pascal
procedure MoveDown(AElement: IwbElement);
```

## Description

Moves the element down one position (toward a higher index) within its parent container.

This function calls the element's MoveDown method, which swaps the element with the next element in the container. Only works for elements in arrays or sorted containers. The element must not already be at the last position. Use CanMoveDown first to verify the operation is valid, otherwise the method may have no effect or raise an exception.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to move down in its array |

## Example

```pascal
var
    element: IwbElement;
begin
    if CanMoveDown(element) then
        MoveDown(element);
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)
- [CanMoveUp](IwbElement_CanMoveUp.md)


