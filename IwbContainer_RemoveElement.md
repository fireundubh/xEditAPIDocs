# RemoveElement

## Syntax

```pascal
function RemoveElement(AContainer: IwbContainer; AChild: Variant): IwbElement;
```

## Description

Removes a child element from the container by index, name, or element reference.

This function calls the container's RemoveElement method with flexible input handling. It accepts an integer (removes by index), string (removes by name), or IwbElement (removes specific element instance). Returns the removed element. The element is detached from the container but the reference remains valid until all references are released. Indices and element positions may shift after removal.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to remove the element from |
| AChild | Variant | The element or element name to remove |

## Returns

Returns the removed element as an IwbElement interface.

## Example

```pascal
// Example 1: Remove element by name
var
  removedElement: IwbElement;
begin
  if Assigned(e) then begin
    removedElement := RemoveElement(e, 'Model');
    if Assigned(removedElement) then
      AddMessage('Removed Model element')
    else
      AddMessage('No Model element to remove');
  end;
end;

// Example 2: Remove element by index (variant accepts integer)
var
  keywords: IwbContainer;
  removedKeyword: IwbElement;
  keywordValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      // Remove first keyword (index 0)
      removedKeyword := RemoveElement(keywords, 0);
      if Assigned(removedKeyword) then begin
        keywordValue := GetEditValue(removedKeyword);
        AddMessage('Removed keyword: ' + keywordValue);
      end;
    end;
  end;
end;

// Example 3: Remove element by reference
var
  conditions: IwbContainer;
  condition, removedCondition: IwbElement;
  functionName: string;
  i, count: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      count := ElementCount(conditions);
      BeginUpdate(conditions);
      try
        // Remove all conditions with specific function
        for i := count - 1 downto 0 do begin
          condition := ElementByIndex(conditions, i);
          if Assigned(condition) then begin
            functionName := GetElementEditValue(condition, 'CTDA\Function');
            if functionName = 'GetItemCount' then begin
              removedCondition := RemoveElement(conditions, condition);
              if Assigned(removedCondition) then
                AddMessage(Format('Removed condition at index %d', [i]));
            end;
          end;
        end;
      finally
        EndUpdate(conditions);
      end;
    end;
  end;
end;

// Example 4: Remove and transfer element
var
  targetRec: IwbMainRecord;
  sourceKeywords, targetKeywords: IwbContainer;
  keyword, removedKeyword: IwbElement;
begin
  targetRec := RecordByFormID(FileByIndex(0), $00012345, True);

  if Assigned(e) and Assigned(targetRec) then begin
    sourceKeywords := ElementByPath(e, 'KWDA');
    targetKeywords := ElementByPath(targetRec, 'KWDA');

    if Assigned(sourceKeywords) and Assigned(targetKeywords) then begin
      if ElementCount(sourceKeywords) > 0 then begin
        keyword := ElementByIndex(sourceKeywords, 0);
        if Assigned(keyword) then begin
          // Remove from source
          removedKeyword := RemoveElement(sourceKeywords, keyword);
          // Add to target
          AddElement(targetKeywords, removedKeyword);
          AddMessage('Transferred keyword to target record');
        end;
      end;
    end;
  end;
end;
```

## See Also

- [Add](IwbContainer_Add.md)
- [AddElement](IwbContainer_AddElement.md)
- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [Remove](IwbElement_Remove.md)


