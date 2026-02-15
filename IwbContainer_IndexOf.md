# IndexOf

## Syntax

```pascal
function IndexOf(AContainer: IwbContainer; AElement: IwbElement): integer;
```

## Description

Searches for an element within the container and returns its zero-based index position.

This function calls the container's IndexOf method with the element to search for. Returns the index (0 to ElementCount-1) if found, or -1 if the element is not a child of this container. Useful for determining element position before operations like MoveUp/MoveDown, or for checking container membership. The search is by element identity (same instance), not by value comparison.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| AElement | IwbElement | The element to find the index of |

## Returns

Returns the zero-based index of the element, or -1 if not found.

## Example

```pascal
// Example 1: Find element position in array
var
  keywords: IwbContainer;
  keyword: IwbElement;
  keywordIndex: integer;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      keyword := ElementByIndex(keywords, 0);
      if Assigned(keyword) then begin
        keywordIndex := IndexOf(keywords, keyword);
        AddMessage(Format('Keyword position: %d', [keywordIndex]));
      end;
    end;
  end;
end;

// Example 2: Check if element belongs to container
var
  keywords: IwbContainer;
  conditions: IwbContainer;
  element: IwbElement;
  inKeywords, inConditions: boolean;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    conditions := ElementByPath(e, 'Conditions');
    element := ElementByPath(e, 'KWDA\[0]');

    if Assigned(keywords) and Assigned(element) then begin
      inKeywords := IndexOf(keywords, element) >= 0;
      AddMessage(Format('Element is in keywords: %s', [BoolToStr(inKeywords, True)]));
    end;

    if Assigned(conditions) and Assigned(element) then begin
      inConditions := IndexOf(conditions, element) >= 0;
      AddMessage(Format('Element is in conditions: %s', [BoolToStr(inConditions, True)]));
    end;
  end;
end;

// Example 3: Remove element by searching for it
var
  keywords: IwbContainer;
  targetKeyword: IwbElement;
  keywordIndex: integer;
  i, count: integer;
  keyword: IwbElement;
  keywordValue: string;
  targetValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      targetValue := '00012345';
      count := ElementCount(keywords);

      // Find keyword with specific value
      for i := 0 to count - 1 do begin
        keyword := ElementByIndex(keywords, i);
        if Assigned(keyword) then begin
          keywordValue := GetEditValue(keyword);
          if keywordValue = targetValue then begin
            targetKeyword := keyword;
            Break;
          end;
        end;
      end;

      // Remove if found
      if Assigned(targetKeyword) then begin
        keywordIndex := IndexOf(keywords, targetKeyword);
        if keywordIndex >= 0 then begin
          AddMessage(Format('Removing keyword at position %d', [keywordIndex]));
          RemoveByIndex(keywords, keywordIndex);
        end;
      end else
        AddMessage('Target keyword not found');
    end;
  end;
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementExists](IwbContainer_ElementExists.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [ElementCount](IwbContainer_ElementCount.md)


