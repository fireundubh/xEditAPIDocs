# IsSorted

## Syntax

```pascal
function IsSorted(AContainer: IwbSortableContainer): boolean;
```

## Description

Checks whether the container automatically maintains its elements in sorted order.

This function retrieves the Sorted property from an IwbSortableContainer, which returns true if the container's definition requires elements to be kept in a specific order (by sort key). Sorted containers automatically reorder elements when they're added or modified. Manual reordering with MoveUp/MoveDown typically doesn't work on sorted containers. Returns false for an unsorted container and for anything that is not a sortable container (a main record, group, or plain struct, for example). Arrays, subrecord arrays, subrecords, and values are the types that can return true.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbSortableContainer | The sortable container to check |

## Returns

Returns true if the container maintains sorted order, false otherwise.

## Example

```pascal
// Example 1: Check an array before reordering it
var
  keywords: IwbContainer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      if IsSorted(keywords) then
        AddMessage('Keyword array is sorted')
      else
        AddMessage('Keyword array is not sorted');
    end;
  end;
end;

// Example 2: Only reverse when the container is not sorted
var
  conditions: IwbContainer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      if not IsSorted(conditions) then begin
        AddMessage('Reversing unsorted container');
        ReverseElements(conditions);
      end else
        AddMessage('Skipping sorted container');
    end;
  end;
end;

// Example 3: Check sort state before moving a child
var
  keywords: IwbContainer;
  element: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      element := ElementByIndex(keywords, 0);
      if IsSorted(keywords) then
        AddMessage('Cannot rely on manual order in a sorted container')
      else if Assigned(element) and CanMoveDown(element) then
        AddMessage('Element can be moved down')
      else
        AddMessage('Element is already at the bottom, or is not assigned');
    end;
  end;
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [CanMoveUp](IwbElement_CanMoveUp.md)
- [ContainerStates](IwbContainer_ContainerStates.md)


