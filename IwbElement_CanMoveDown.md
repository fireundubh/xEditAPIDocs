# CanMoveDown

## Syntax

```pascal
function CanMoveDown(AElement: IwbElement): boolean;
```

## Description

Checks whether the element can be moved down (toward higher indices) within its parent container.

This function retrieves the CanMoveDown property, which returns true if the element is part of an array or sorted container and is not already at the last position. Returns false if the element is invalid, not in a moveable container, or already at the end. Always check this before calling MoveDown to avoid errors.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check |

## Returns

Returns `true` if the element is part of an array and can be moved down to a lower index position.

## Example

```pascal
var
  element: IwbElement;
begin
  if CanMoveDown(element) then
    // Proceed with moving the element down
end;
```

## See Also

- [CanMoveUp](IwbElement_CanMoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)


