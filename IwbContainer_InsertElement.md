# InsertElement

## Syntax

```pascal
procedure InsertElement(AContainer: IwbContainer; AIndex: Integer; AElement: IwbElement);
```

## Description

Inserts a new element at the specified index position in the container.

This procedure creates a new element with the given signature and inserts it at the specified index. All existing elements at and after the index are shifted right.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to insert the element into |
| AIndex | Integer | The zero-based index position to insert at |
| AElement | IwbElement | The element to insert |

## Example

```pascal
// Example 1: Insert element at beginning of array
var
  keywords: IwbContainer;
  newKeyword, existingKeyword: IwbElement;
  keywordValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      // Create new keyword element
      newKeyword := Add(keywords, 'Keyword', True);
      if Assigned(newKeyword) then begin
        SetEditValue(newKeyword, '00012345');
        // Remove from end and insert at beginning
        existingKeyword := RemoveElement(keywords, newKeyword);
        InsertElement(keywords, 0, existingKeyword);
        AddMessage('Inserted keyword at position 0');
      end;
    end;
  end;
end;

// Example 2: Insert element at specific position
var
  conditions: IwbContainer;
  newCondition, removedCondition: IwbElement;
  insertIndex: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      // Create new condition
      newCondition := Add(conditions, 'Condition', True);
      if Assigned(newCondition) then begin
        SetElementEditValue(newCondition, 'CTDA\Type', '10000000');
        SetElementEditValue(newCondition, 'CTDA\Comparison Value', '1');

        // Insert at position 2 (third position)
        insertIndex := 2;
        if insertIndex <= ElementCount(conditions) then begin
          removedCondition := RemoveElement(conditions, newCondition);
          InsertElement(conditions, insertIndex, removedCondition);
          AddMessage(Format('Inserted condition at position %d', [insertIndex]));
        end;
      end;
    end;
  end;
end;

// Example 3: Reorder array by moving element
var
  effects: IwbContainer;
  effect, removedEffect: IwbElement;
  fromIndex, toIndex: integer;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) and (ElementCount(effects) > 3) then begin
      BeginUpdate(effects);
      try
        fromIndex := 3;
        toIndex := 1;

        // Move element from position 3 to position 1
        effect := ElementByIndex(effects, fromIndex);
        if Assigned(effect) then begin
          removedEffect := RemoveElement(effects, effect);
          InsertElement(effects, toIndex, removedEffect);
          AddMessage(Format('Moved effect from %d to %d', [fromIndex, toIndex]));
        end;
      finally
        EndUpdate(effects);
      end;
    end;
  end;
end;
```

## See Also

- [Add](IwbContainer_Add.md)
- [AddElement](IwbContainer_AddElement.md)
- [RemoveElement](IwbContainer_RemoveElement.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)


