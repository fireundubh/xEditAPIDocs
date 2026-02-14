# CanMoveDown

## Syntax

```pascal
function CanMoveDown(AElement: IwbElement): boolean;
```

## Description

Determines if an element can be moved down within its array.

Returns `true` if the element is part of an array and can be moved further down using `MoveDown`. This is typically used to check if an element's position can be changed within its containing array.

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


