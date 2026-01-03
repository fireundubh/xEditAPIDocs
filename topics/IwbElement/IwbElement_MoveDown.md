# MoveDown

## Syntax

```pascal
procedure MoveDown(AElement: IwbElement);
```

## Description

Moves an element down by one slot in an array.

Only works if the element is part of an array. Should be used after checking if the movement is possible.

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
