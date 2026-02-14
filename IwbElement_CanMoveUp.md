# CanMoveUp

## Syntax

```pascal
function CanMoveUp(AElement: IwbElement): boolean;
```

## Description

Determines if an element can be moved up within its array.

Returns `true` if the element is part of an array and can be moved further up using `MoveUp`. This function is used to verify if an element's position can be changed within its containing array.

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


