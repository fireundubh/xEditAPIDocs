# MoveUp

## Syntax

```pascal
procedure MoveUp(AElement: IwbElement);
```

## Description

Moves the element up one position (toward a lower index) within its parent container.

This function calls the element's MoveUp method, which swaps the element with the previous element in the container. Only works for elements in arrays or sorted containers. The element must not already be at the first position. Use CanMoveUp first to verify the operation is valid, otherwise the method may have no effect or raise an exception.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to move up in its array |

## Example

```pascal
// Example 1: Move single element up with validation
var
  keywords: IwbContainer;
  element: IwbElement;
  oldIndex: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      element := ElementByIndex(keywords, 2);
      if Assigned(element) then begin
        oldIndex := 2;
        if CanMoveUp(element) then begin
          MoveUp(element);
          AddMessage(Format('Moved keyword from index %d to %d', [oldIndex, oldIndex - 1]));
        end;
      end;
    end;
  end;
end;

// Example 2: Prioritize specific condition
var
  conditions: IwbContainer;
  i: integer;
  condition, funcElement: IwbElement;
  funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      // Find GetDead condition and move to top
      for i := ElementCount(conditions) - 1 downto 0 do begin
        condition := ElementByIndex(conditions, i);
        if Assigned(condition) then begin
          funcElement := ElementByPath(condition, 'CTDA\Function');
          if Assigned(funcElement) then begin
            funcValue := GetEditValue(funcElement);
            if funcValue = 'GetDead' then begin
              while CanMoveUp(condition) do
                MoveUp(condition);
              AddMessage('Moved GetDead condition to top');
              Break;
            end;
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Swap adjacent elements
var
  keywords: IwbContainer;
  element1, element2: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) >= 2) then begin
      element2 := ElementByIndex(keywords, 1);
      if Assigned(element2) and CanMoveUp(element2) then begin
        MoveUp(element2);
        AddMessage('Swapped keywords at indices 0 and 1');
      end;
    end;
  end;
end;
```

## See Also

- [CanMoveUp](IwbElement_CanMoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)
- [CanMoveDown](IwbElement_CanMoveDown.md)


