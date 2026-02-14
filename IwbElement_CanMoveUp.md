# CanMoveUp

## Syntax

```pascal
function CanMoveUp(AElement: IwbElement): boolean;
```

## Description

Checks whether the element can be moved up (toward lower indices) within its parent container.

This function retrieves the CanMoveUp property, which returns true if the element is part of an array or sorted container and is not already at the first position. Returns false if the element is invalid, not in a moveable container, or already at the beginning. Always check this before calling MoveUp to avoid errors.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check if it can be moved up |

## Returns

Returns true if the element can be moved up in its array, false otherwise.

## Example

```pascal
var
  element: IwbElement;
begin
  if CanMoveUp(element) then
    // Proceed with moving the element up
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)


