# IsSorted

## Syntax

```pascal
function IsSorted(AContainer: IwbSortableContainer): boolean;
```

## Description

Checks whether the container automatically maintains its elements in sorted order.

This function retrieves the Sorted property from an IwbSortableContainer, which returns true if the container's definition requires elements to be kept in a specific order (by sort key). Sorted containers automatically reorder elements when they're added or modified. Manual reordering with MoveUp/MoveDown typically doesn't work on sorted containers. Returns false for unsorted containers or invalid inputs.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbSortableContainer | The sortable container to check |

## Returns

Returns true if the container maintains sorted order, false otherwise.

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [CanMoveUp](IwbElement_CanMoveUp.md)
- [ContainerStates](IwbContainer_ContainerStates.md)


