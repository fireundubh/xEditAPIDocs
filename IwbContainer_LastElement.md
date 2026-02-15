# LastElement

## Syntax

```pascal
function LastElement(AContainer: IwbContainer): IwbElement;
```

## Description

Returns the last element in the container, or nil if there are no children.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to get the last element from |

## Returns

Returns the last element as an IwbElement interface, or nil if the container is empty.

## Example

```pascal
// Example 1: Get last keyword in array
var
  keywords: IwbContainer;
  lastKeyword: IwbElement;
  keywordValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      lastKeyword := LastElement(keywords);
      if Assigned(lastKeyword) then begin
        keywordValue := GetEditValue(lastKeyword);
        AddMessage('Last keyword: ' + keywordValue);
      end else
        AddMessage('No keywords in array');
    end;
  end;
end;

// Example 2: Compare first and last elements
var
  conditions: IwbContainer;
  firstCondition, lastCondition: IwbElement;
  firstValue, lastValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      if ElementCount(conditions) > 0 then begin
        firstCondition := ElementByIndex(conditions, 0);
        lastCondition := LastElement(conditions);

        if Assigned(firstCondition) and Assigned(lastCondition) then begin
          firstValue := GetElementEditValue(firstCondition, 'CTDA\Comparison Value');
          lastValue := GetElementEditValue(lastCondition, 'CTDA\Comparison Value');
          AddMessage(Format('First condition value: %s, Last: %s',
            [firstValue, lastValue]));
        end;
      end;
    end;
  end;
end;

// Example 3: Remove last element from array
var
  effects: IwbContainer;
  lastEffect: IwbElement;
  count: integer;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      count := ElementCount(effects);
      if count > 0 then begin
        lastEffect := LastElement(effects);
        if Assigned(lastEffect) then begin
          AddMessage(Format('Removing last effect (%d of %d)', [count, count]));
          RemoveElement(effects, lastEffect);
        end;
      end else
        AddMessage('No effects to remove');
    end;
  end;
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementCount](IwbContainer_ElementCount.md)


