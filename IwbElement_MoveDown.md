# MoveDown

## Syntax

```pascal
procedure MoveDown(AElement: IwbElement);
```

## Description

Moves the element down one position (toward a higher index) within its parent container.

This function calls the element's MoveDown method, which swaps the element with the next element in the container. Only works for elements in arrays or sorted containers. The element must not already be at the last position. Use CanMoveDown first to verify the operation is valid, otherwise the method may have no effect or raise an exception.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to move down in its array |

## Example

```pascal
// Example 1: Move single element down with validation
var
  keywords: IwbContainer;
  element: IwbElement;
  oldIndex: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      element := ElementByIndex(keywords, 0);
      if Assigned(element) then begin
        oldIndex := 0;
        if CanMoveDown(element) then begin
          MoveDown(element);
          AddMessage(Format('Moved keyword from index %d to %d', [oldIndex, oldIndex + 1]));
        end;
      end;
    end;
  end;
end;

// Example 2: Deprioritize specific condition
var
  conditions: IwbContainer;
  i: integer;
  condition, funcElement: IwbElement;
  funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      // Find GetQuestRunning condition and move to end
      for i := 0 to ElementCount(conditions) - 1 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          funcElement := ElementByPath(condition, 'CTDA\Function');
          if Assigned(funcElement) then begin
            funcValue := GetEditValue(funcElement);
            if funcValue = 'GetQuestRunning' then begin
              while CanMoveDown(condition) do
                MoveDown(condition);
              AddMessage('Moved GetQuestRunning condition to end');
              Break;
            end;
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Reverse array order
var
  keywords: IwbContainer;
  element: IwbElement;
  i, count: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      count := ElementCount(keywords);
      for i := 0 to count - 2 do begin
        element := ElementByIndex(keywords, 0);
        if Assigned(element) then begin
          while CanMoveDown(element) do
            MoveDown(element);
        end;
      end;
      AddMessage(Format('Reversed order of %d keywords', [count]));
    end;
  end;
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)
- [CanMoveUp](IwbElement_CanMoveUp.md)


