# Name

## Syntax

```pascal
function Name(AElement: IwbElement): string;
```

## Description

Returns the element's standard name as defined in its element definition.

This function retrieves the Name property, which returns the element's identifier from the record structure definition. For fields, this is typically the 4-character signature (e.g., "EDID", "DATA"). For array elements, it may include an index. Returns an empty string if the element is invalid. This is the most commonly used name function for element identification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose name to retrieve |

## Returns

Returns the standard name of the element as a string.

## Example

```pascal
// Example 1: Iterate record elements and log their names
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  elementName: string;
begin
  if Assigned(e) then begin
    container := e;
    AddMessage('Elements in ' + EditorID(e) + ':');
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        elementName := Name(element);
        AddMessage(Format('  [%d] %s = %s', [i, elementName, GetEditValue(element)]));
      end;
    end;
  end;
end;

// Example 2: Find elements with specific signature
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  elementName: string;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        elementName := Name(element);
        if elementName = 'MODL' then
          AddMessage('Found model path: ' + GetEditValue(element));
      end;
    end;
  end;
end;

// Example 3: Build dynamic element access
var
  keywords: IwbContainer;
  i: integer;
  kwdElement: IwbElement;
  kwdName: string;
begin
  if Assigned(e) then begin
    keywords := ElementByPath(e, 'KWDA');
    if Assigned(keywords) then begin
      for i := 0 to ElementCount(keywords) - 1 do begin
        kwdElement := ElementByIndex(keywords, i);
        if Assigned(kwdElement) then begin
          kwdName := Name(kwdElement);
          AddMessage(Format('Keyword element name: %s (index %d)', [kwdName, i]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [BaseName](IwbElement_BaseName.md)
- [ShortName](IwbElement_ShortName.md)
- [DisplayName](IwbElement_DisplayName.md)
- [PathName](IwbElement_PathName.md)
- [Path](IwbElement_Path.md)


