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

## Example

```pascal
// Example 1: Check if container can be manually reordered
var
  container: IwbContainer;
  sortableContainer: IwbSortableContainer;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'KWDA');
    if Assigned(container) then begin
      if Supports(container, IwbSortableContainer, sortableContainer) then begin
        if IsSorted(sortableContainer) then
          AddMessage('Container is auto-sorted, manual reordering not available')
        else
          AddMessage('Container is unsorted, can be manually reordered');
      end else
        AddMessage('Container does not support sorting operations');
    end;
  end;
end;

// Example 2: Only reverse if not sorted
var
  conditions: IwbContainer;
  sortableContainer: IwbSortableContainer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      if Supports(conditions, IwbSortableContainer, sortableContainer) then begin
        if not IsSorted(sortableContainer) then begin
          AddMessage('Reversing unsorted container');
          ReverseElements(conditions);
        end else
          AddMessage('Skipping sorted container (would auto-reorder)');
      end;
    end;
  end;
end;

// Example 3: Check sortability before move operations
var
  container: IwbContainer;
  element: IwbElement;
  sortableContainer: IwbSortableContainer;
  canMove: boolean;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'KWDA');
    if Assigned(container) and (ElementCount(container) > 0) then begin
      element := ElementByIndex(container, 0);

      canMove := True;
      if Supports(container, IwbSortableContainer, sortableContainer) then
        canMove := not IsSorted(sortableContainer);

      if canMove then begin
        if CanMoveDown(element) then
          AddMessage('Element can be moved down')
        else
          AddMessage('Element is already at bottom');
      end else
        AddMessage('Cannot move elements in sorted container');
    end;
  end;
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [CanMoveUp](IwbElement_CanMoveUp.md)
- [ContainerStates](IwbContainer_ContainerStates.md)


