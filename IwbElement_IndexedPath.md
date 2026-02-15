# IndexedPath

## Syntax

```pascal
function IndexedPath(AElement: IwbElement; AIncludeMainRecord: Boolean): String;
```

## Description

Returns the indexed path of `AElement`. If `AIncludeMainRecord` is true, the path starts from the main record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the indexed path from |
| AIncludeMainRecord | Boolean | Whether to include the main record in the path |

## Returns

Returns the indexed path as a string.

## Example

```pascal
// Example 1: Get indexed path from main record
var
  rec: IwbMainRecord;
  element: IwbElement;
  indexedPath: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      indexedPath := IndexedPath(element, True);
      AddMessage(Format('Indexed path with record: %s', [indexedPath]));
      // Output: "WEAP\[0]\DATA\Value" (index relative to main record)
    end;
  end;
end;

// Example 2: Compare paths with and without main record
var
  rec: IwbMainRecord;
  element: IwbElement;
  pathWithRecord, pathWithoutRecord: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'Conditions\[0]\CTDA\Function');
    if Assigned(element) then begin
      pathWithRecord := IndexedPath(element, True);
      pathWithoutRecord := IndexedPath(element, False);
      AddMessage('With record: ' + pathWithRecord);
      AddMessage('Without record: ' + pathWithoutRecord);
    end;
  end;
end;

// Example 3: Use indexed path for ElementByIndexedPath lookup
var
  rec: IwbMainRecord;
  originalElement, foundElement: IwbElement;
  indexedPath: string;
  value1, value2: string;
begin
  if Assigned(e) then begin
    originalElement := ElementByPath(e, 'KWDA\[2]');
    if Assigned(originalElement) then begin
      indexedPath := IndexedPath(originalElement, True);
      AddMessage('Original path: ' + indexedPath);

      // Use the indexed path to relocate the element
      foundElement := ElementByIndexedPath(rec, indexedPath);
      if Assigned(foundElement) then begin
        value1 := GetEditValue(originalElement);
        value2 := GetEditValue(foundElement);
        if value1 = value2 then
          AddMessage('Successfully found element using indexed path')
        else
          AddMessage('ERROR: Values do not match');
      end;
    end;
  end;
end;
```

## See Also

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)
