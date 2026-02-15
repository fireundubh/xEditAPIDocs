# CanMoveDown

## Syntax

```pascal
function CanMoveDown(AElement: IwbElement): boolean;
```

## Description

Checks whether the element can be moved down (toward higher indices) within its parent container.

This function retrieves the CanMoveDown property, which returns true if the element is part of an array or sorted container and is not already at the last position. Returns false if the element is invalid, not in a moveable container, or already at the end. Always check this before calling MoveDown to avoid errors.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check |

## Returns

Returns `true` if the element is part of an array and can be moved down to a lower index position.

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
      element := ElementByIndex(keywords, 0);
      if Assigned(element) and CanMoveDown(element) then begin
        MoveDown(element);
        AddMessage(Format('Moved keyword down in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Move element to end of array
var
  conditions: IwbContainer;
  element: IwbElement;
  moveCount: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      element := ElementByIndex(conditions, 0);
      if Assigned(element) then begin
        moveCount := 0;
        while CanMoveDown(element) do begin
          MoveDown(element);
          Inc(moveCount);
        end;
        AddMessage(Format('Moved condition to end (%d moves)', [moveCount]));
      end;
    end;
  end;
end;

// Example 3: Check movement boundaries
var
  keywords: IwbContainer;
  i: integer;
  element: IwbElement;
  canMoveUp, canMoveDown: boolean;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      for i := 0 to ElementCount(keywords) - 1 do begin
        element := ElementByIndex(keywords, i);
        if Assigned(element) then begin
          canMoveUp := CanMoveUp(element);
          canMoveDown := CanMoveDown(element);
          AddMessage(Format('[%d] Up: %s, Down: %s',
            [i, BoolToStr(canMoveUp, True), BoolToStr(canMoveDown, True)]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [CanMoveUp](IwbElement_CanMoveUp.md)
- [MoveDown](IwbElement_MoveDown.md)
- [MoveUp](IwbElement_MoveUp.md)


