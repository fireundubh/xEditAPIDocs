# ElementByIndex

## Syntax

```pascal
function ElementByIndex(AContainer: IwbContainer; AIndex: integer): IwbElement;
```

## Description

Returns the element at the specified zero-based index within the container.

This function accesses the Elements property by index, which provides direct array-style access to child elements. Index 0 returns the first element, index 1 the second, and so on. Returns nil if the index is out of bounds (negative or >= ElementCount). No exception is raised for invalid indices.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the element from |
| AIndex | integer | The zero-based index of the element to retrieve |

## Returns

Returns the element at the specified index as an IwbElement interface.

## Example

```pascal
// Example 1: Iterate through all keywords
var
  keywords: IwbContainer;
  i, count: integer;
  keyword: IwbElement;
  keywordValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      count := ElementCount(keywords);
      AddMessage(Format('Iterating through %d keywords:', [count]));

      for i := 0 to count - 1 do begin
        keyword := ElementByIndex(keywords, i);
        if Assigned(keyword) then begin
          keywordValue := GetEditValue(keyword);
          AddMessage(Format('  [%d] %s', [i, keywordValue]));
        end;
      end;
    end;
  end;
end;

// Example 2: Access specific array element by index
var
  conditions: IwbContainer;
  secondCondition: IwbElement;
  functionName: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) and (ElementCount(conditions) > 1) then begin
      // Get second condition (index 1)
      secondCondition := ElementByIndex(conditions, 1);
      if Assigned(secondCondition) then begin
        functionName := GetElementEditValue(secondCondition, 'CTDA\Function');
        AddMessage('Second condition function: ' + functionName);
      end;
    end else
      AddMessage('Need at least 2 conditions');
  end;
end;

// Example 3: Safe iteration with bounds checking
var
  effects: IwbContainer;
  i, count: integer;
  effect: IwbElement;
  magnitude: string;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      count := ElementCount(effects);
      if count = 0 then begin
        AddMessage('No effects to process');
        Exit;
      end;

      for i := 0 to count - 1 do begin
        effect := ElementByIndex(effects, i);
        if Assigned(effect) then begin
          magnitude := GetElementEditValue(effect, 'EFIT\Magnitude');
          AddMessage(Format('Effect %d magnitude: %s', [i, magnitude]));
        end else
          AddMessage(Format('Warning: Effect at index %d is nil', [i]));
      end;
    end;
  end;
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [IndexOf](IwbContainer_IndexOf.md)
- [LastElement](IwbContainer_LastElement.md)


