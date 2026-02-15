# RemoveByIndex

## Syntax

```pascal
function RemoveByIndex(AContainer: IwbContainer; AIndex: integer; AMarkModified: boolean): IwbElement;
```

## Description

Removes and returns the element at the specified index in the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to remove the element from |
| AIndex | integer | The zero-based index of the element to remove |
| AMarkModified | boolean | If true, marks the container as modified |

## Returns

Returns the removed element as an IwbElement interface.

## Example

```pascal
// Example 1: Remove first element
var
  keywords: IwbContainer;
  removed: IwbElement;
  keywordValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      removed := RemoveByIndex(keywords, 0, True);
      if Assigned(removed) then begin
        keywordValue := GetEditValue(removed);
        AddMessage('Removed first keyword: ' + keywordValue);
      end;
    end;
  end;
end;

// Example 2: Remove last element
var
  conditions: IwbContainer;
  removed: IwbElement;
  lastIndex: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      lastIndex := ElementCount(conditions) - 1;
      if lastIndex >= 0 then begin
        removed := RemoveByIndex(conditions, lastIndex, True);
        if Assigned(removed) then
          AddMessage(Format('Removed last condition (was at index %d)', [lastIndex]));
      end;
    end;
  end;
end;

// Example 3: Remove multiple elements by index (reverse iteration)
var
  effects: IwbContainer;
  removed: IwbElement;
  i, count: integer;
  magnitude: string;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      count := ElementCount(effects);
      BeginUpdate(effects);
      try
        // Remove all effects with magnitude 0 (iterate backwards to avoid index shift issues)
        for i := count - 1 downto 0 do begin
          magnitude := GetElementEditValue(ElementByIndex(effects, i), 'EFIT\Magnitude');
          if magnitude = '0' then begin
            removed := RemoveByIndex(effects, i, False);
            if Assigned(removed) then
              AddMessage(Format('Removed effect at index %d', [i]));
          end;
        end;
      finally
        EndUpdate(effects);
      end;
    end;
  end;
end;

// Example 4: Remove with and without modification flag
var
  keywords: IwbContainer;
  removed: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) and (ElementCount(keywords) > 0) then begin
      // Remove without marking as modified (temporary operation)
      removed := RemoveByIndex(keywords, 0, False);
      if Assigned(removed) then begin
        AddMessage('Removed element without marking modified');
        // Can be re-added later if needed
        AddElement(keywords, removed);
      end;
    end;
  end;
end;
```

## See Also

- [RemoveElement](IwbContainer_RemoveElement.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [Remove](IwbElement_Remove.md)


