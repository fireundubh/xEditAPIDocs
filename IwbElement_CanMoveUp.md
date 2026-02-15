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
// Example 1: Safe element reordering
var
  keywords: IwbContainer;
  element: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 1) then begin
      element := ElementByIndex(keywords, 1);
      if Assigned(element) and CanMoveUp(element) then begin
        MoveUp(element);
        AddMessage(Format('Moved keyword up in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Move element to top of array
var
  conditions: IwbContainer;
  element: IwbElement;
  moveCount: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      element := ElementByIndex(conditions, 3);
      if Assigned(element) then begin
        moveCount := 0;
        while CanMoveUp(element) do begin
          MoveUp(element);
          Inc(moveCount);
        end;
        AddMessage(Format('Moved condition to top (%d moves)', [moveCount]));
      end;
    end;
  end;
end;

// Example 3: Validate before batch reordering
var
  keywords: IwbContainer;
  i: integer;
  element: IwbElement;
  movableCount: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      movableCount := 0;
      for i := 0 to ElementCount(keywords) - 1 do begin
        element := ElementByIndex(keywords, i);
        if Assigned(element) and CanMoveUp(element) then
          Inc(movableCount);
      end;
      AddMessage(Format('%d of %d keywords can move up',
        [movableCount, ElementCount(keywords)]));
    end;
  end;
end;
```

## See Also

- [CanMoveDown](IwbElement_CanMoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)


