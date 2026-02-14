# MoveUp

## Syntax

```pascal
procedure MoveUp(AElement: IwbElement);
```

## Description

Moves an element up by one slot in an array.

Only works if the element is part of an array. Should be used after checking if the movement is possible.

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


