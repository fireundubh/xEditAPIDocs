# AddElement

## Syntax

```pascal
procedure AddElement(AContainer: IwbContainer; AElement: IwbElement);
```

## Description

Adds an existing element instance to the container.

This procedure calls the container's AddElement method, which takes ownership of an already-created element and adds it to the container's child list. The element is typically moved from another location or created separately. This is a lower-level operation compared to Add, which creates new elements. Use when you need to transfer elements between containers or work with pre-constructed elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to add the element to |
| AElement | IwbElement | The element to add to the container |

## Example

```pascal
// Example 1: Move element from one container to another
var
  rec: IwbMainRecord;
  sourceContainer, targetContainer: IwbContainer;
  element: IwbElement;
  removedElement: IwbElement;
begin
  if Assigned(e) then begin
    sourceContainer := ElementByPath(e, 'Conditions');
    targetContainer := ElementByPath(e, 'KWDA');

    if Assigned(sourceContainer) and Assigned(targetContainer) then begin
      if ElementCount(sourceContainer) > 0 then begin
        element := ElementByIndex(sourceContainer, 0);
        if Assigned(element) then begin
          // Remove from source
          removedElement := RemoveElement(sourceContainer, element);
          // Add to target
          AddElement(targetContainer, removedElement);
          AddMessage('Moved element between containers');
        end;
      end;
    end;
  end;
end;

// Example 2: Transfer elements using Add + AddElement pattern
var
  targetRec: IwbMainRecord;
  sourceKeywords, targetKeywords: IwbContainer;
  i, count: integer;
  keyword, newKeyword: IwbElement;
  keywordValue: string;
begin
  targetRec := RecordByFormID(FileByIndex(0), $00012345, True);

  if Assigned(e) and Assigned(targetRec) then begin
    sourceKeywords := ElementByPath(e, 'KWDA');
    targetKeywords := ElementByPath(targetRec, 'KWDA');

    if Assigned(sourceKeywords) and Assigned(targetKeywords) then begin
      count := ElementCount(sourceKeywords);
      BeginUpdate(targetKeywords);
      try
        for i := 0 to count - 1 do begin
          keyword := ElementByIndex(sourceKeywords, i);
          if Assigned(keyword) then begin
            keywordValue := GetEditValue(keyword);
            // Create new element in target
            newKeyword := Add(targetKeywords, 'Keyword', True);
            if Assigned(newKeyword) then
              SetEditValue(newKeyword, keywordValue);
          end;
        end;
        AddMessage(Format('Copied %d keywords to target', [count]));
      finally
        EndUpdate(targetKeywords);
      end;
    end;
  end;
end;

// Example 3: Reorganize array elements (low-level reordering)
var
  rec: IwbMainRecord;
  container: IwbContainer;
  lastElement, removedElement: IwbElement;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'KWDA');
    if Assigned(container) and (ElementCount(container) > 1) then begin
      BeginUpdate(container);
      try
        // Move last element to first position
        lastElement := LastElement(container);
        if Assigned(lastElement) then begin
          removedElement := RemoveElement(container, lastElement);
          InsertElement(container, 0, removedElement);
          AddMessage('Moved last element to first position');
        end;
      finally
        EndUpdate(container);
      end;
    end;
  end;
end;
```

## See Also

- [Add](IwbContainer_Add.md)
- [InsertElement](IwbContainer_InsertElement.md)
- [RemoveElement](IwbContainer_RemoveElement.md)


