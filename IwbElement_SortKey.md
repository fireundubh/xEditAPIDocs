# SortKey

## Syntax

```pascal
function SortKey(AElement: IwbElement; AExtended: Boolean): string;
```

## Description

Returns the string xEdit uses when it sorts `AElement`. Both arguments are required. `False` is the normal sort key. `True` asks for the extended key, which some value definitions build differently. A main record's key is its FormID either way.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | Element to get the sort key for |
| AExtended | Boolean | `False` for the normal key, `True` for the extended key |

## Returns

Returns the sort key as a string.

## Example

```pascal
// Example 1: Sort elements by sort key
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  sortKeys: TStringList;
  sortKey: string;
begin
  if Assigned(e) then begin
    container := e;
    sortKeys := TStringList.Create;
    try
      for i := 0 to ElementCount(container) - 1 do begin
        element := ElementByIndex(container, i);
        if Assigned(element) then begin
          sortKey := SortKey(element, False);
          sortKeys.Add(Format('%s=%s', [sortKey, Name(element)]));
        end;
      end;
      sortKeys.Sort;
      AddMessage('Elements in sort order:');
      for i := 0 to sortKeys.Count - 1 do
        AddMessage('  ' + sortKeys[i]);
    finally
      sortKeys.Free;
    end;
  end;
end;

// Example 2: Compare sort keys for ordering
var
  element1, element2: IwbElement;
  sortKey1, sortKey2: string;
begin
  if Assigned(e) then begin
    element1 := ElementByPath(e, 'EDID');
    element2 := ElementByPath(e, 'FULL');
    if Assigned(element1) and Assigned(element2) then begin
      sortKey1 := SortKey(element1);
      sortKey2 := SortKey(element2);
      if sortKey1 < sortKey2 then
        AddMessage('EDID sorts before FULL')
      else if sortKey1 > sortKey2 then
        AddMessage('FULL sorts before EDID')
      else
        AddMessage('Same sort order');
    end;
  end;
end;

// Example 3: Log sort keys for debugging
var
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  sortKey, editValue: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      AddMessage('Keyword sort keys:');
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) then begin
          sortKey := SortKey(kwdElement, False);
          editValue := GetEditValue(kwdElement);
          AddMessage(Format('  [%d] Key: %s, Value: %s',
            [i, sortKey, editValue]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)


