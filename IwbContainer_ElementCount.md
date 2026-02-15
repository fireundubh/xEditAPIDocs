# ElementCount

## Syntax

```pascal
function ElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns the total number of child elements currently in the container.

This function retrieves the ElementCount property, which returns the count of immediate children only (not recursive). Returns 0 for empty containers or invalid inputs. Use this to iterate through elements with ElementByIndex, or to check if a container has any children. Does not include elements that could be added but haven't been yet.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to count elements in |

## Returns

Returns the total number of elements as an integer.

## Example

```pascal
// Example 1: Iterate through all elements in container
var
  keywords: IwbContainer;
  i, count: integer;
  keyword: IwbElement;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      count := ElementCount(keywords);
      AddMessage(Format('Record has %d keywords', [count]));

      for i := 0 to count - 1 do begin
        keyword := ElementByIndex(keywords, i);
        if Assigned(keyword) then
          AddMessage(Format('  Keyword %d: %s', [i, GetEditValue(keyword)]));
      end;
    end;
  end;
end;

// Example 2: Check if container is empty
var
  conditions: IwbContainer;
  count: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      count := ElementCount(conditions);
      if count = 0 then
        AddMessage('No conditions present')
      else
        AddMessage(Format('Has %d condition(s)', [count]));
    end;
  end;
end;

// Example 3: Process all records in file
var
  plugin: IwbFile;
  i, count: integer;
  rec: IwbMainRecord;
  signature: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    AddMessage(Format('Processing %d records...', [count]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        signature := Signature(rec);
        if signature = 'ARMO' then
          AddMessage(Format('Found armor: %s', [EditorID(rec)]));
      end;
    end;
  end;
end;
```

## See Also

- [AdditionalElementCount](IwbContainer_AdditionalElementCount.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [LastElement](IwbContainer_LastElement.md)


