# PathName

## Syntax

```pascal
function PathName(AElement: IwbElement): string;
```

## Description

Returns the element's path name, combining structural and display information.

This function retrieves the PathName property, which provides a hybrid identifier combining path and name information. The exact format depends on the element type but generally includes the element's position and identifier within its parent. More descriptive than Path alone but not as comprehensive as FullPath. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the combined path and name for |

## Returns

Returns the combined path and name as a string.

## Example

```pascal
// Example 1: Get descriptive element identifier
var
  rec: IwbMainRecord;
  element: IwbElement;
  identifier: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      identifier := PathName(element);
      AddMessage(Format('Element identifier: %s', [identifier]));
      AddMessage(Format('Value: %s', [GetEditValue(element)]));
    end;
  end;
end;

// Example 2: Compare path names for sorting
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  pathNames: TStringList;
begin
  if Assigned(e) then begin
    container := rec;
    pathNames := TStringList.Create;
    try
      for i := 0 to ElementCount(container) - 1 do begin
        element := ElementByIndex(container, i);
        if Assigned(element) then
          pathNames.Add(PathName(element));
      end;
      pathNames.Sort;
      AddMessage('Sorted element path names:');
      for i := 0 to pathNames.Count - 1 do
        AddMessage('  ' + pathNames[i]);
    finally
      pathNames.Free;
    end;
  end;
end;

// Example 3: Log array element path names
var
  rec: IwbMainRecord;
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  kwdPathName: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      AddMessage('Keyword path names in ' + EditorID(rec) + ':');
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) then begin
          kwdPathName := PathName(kwdElement);
          AddMessage(Format('  [%d] %s = %s',
            [i, kwdPathName, GetEditValue(kwdElement)]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [Path](IwbElement_Path.md)
- [FullPath](IwbElement_FullPath.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)


