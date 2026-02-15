# ReverseElements

## Syntax

```pascal
procedure ReverseElements(AContainer: IwbContainer);
```

## Description

Reverses the order of all elements within the specified container.

This procedure modifies the container in-place, changing the order of elements to be the reverse of their current order. The first element becomes the last, and vice versa.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container whose elements to reverse |

## Example

```pascal
// Example 1: Reverse keyword order in array
var
  keywords: IwbContainer;
  i, count: integer;
  keyword: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      count := ElementCount(keywords);
      AddMessage(Format('Reversing %d keywords', [count]));

      ReverseElements(keywords);

      // Show new order
      for i := 0 to count - 1 do begin
        keyword := ElementByIndex(keywords, i);
        if Assigned(keyword) then
          AddMessage(Format('  Position %d: %s', [i, GetEditValue(keyword)]));
      end;
    end;
  end;
end;

// Example 2: Reverse conditions to change evaluation order
var
  conditions: IwbContainer;
  i: integer;
  condition: IwbElement;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      BeginUpdate(conditions);
      try
        AddMessage('Reversing condition evaluation order');
        ReverseElements(conditions);

        // Update condition indices
        for i := 0 to ElementCount(conditions) - 1 do begin
          condition := ElementByIndex(conditions, i);
          if Assigned(condition) then
            AddMessage(Format('Condition %d: %s',
              [i, GetElementEditValue(condition, 'CTDA\Function')]));
        end;
      finally
        EndUpdate(conditions);
      end;
    end;
  end;
end;

// Example 3: Reverse array only if not sorted
var
  container: IwbContainer;
  sortableContainer: IwbSortableContainer;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'KWDA');
    if Assigned(container) then begin
      if Supports(container, IwbSortableContainer, sortableContainer) then begin
        if IsSorted(sortableContainer) then begin
          AddMessage('Cannot reverse sorted container');
          Exit;
        end;
      end;

      AddMessage('Reversing unsorted container');
      ReverseElements(container);
    end;
  end;
end;
```

## See Also

- [AddElement](IwbContainer_AddElement.md)
- [InsertElement](IwbContainer_InsertElement.md)


