# Path

## Syntax

```pascal
function Path(AElement: IwbElement): string;
```

## Description

Returns the element's path segment relative to its parent container.

This function retrieves the Path property, which returns a single component of the element's hierarchical path (typically the element's name). Unlike FullPath, which returns the complete path from the file root, this returns just the immediate path segment. Use when building paths incrementally or when only the local identifier is needed. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the path component for |

## Returns

Returns the path component as a string.

## Example

```pascal
// Example 1: Get local path segment for logging
var
  element: IwbElement;
  pathSegment: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      pathSegment := Path(element);
      AddMessage(Format('Element path segment: %s', [pathSegment]));
      AddMessage(Format('Full path: %s', [FullPath(element)]));
    end;
  end;
end;

// Example 2: Build relative paths during iteration
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  localPath, fullPath: string;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'Conditions');
    if Assigned(container) then begin
      for i := 0 to ElementCount(container) - 1 do begin
        element := ElementByIndex(container, i);
        if Assigned(element) then begin
          localPath := Path(element);
          fullPath := FullPath(element);
          AddMessage(Format('Local: %s | Full: %s', [localPath, fullPath]));
        end;
      end;
    end;
  end;
end;

// Example 3: Compare path components
var
  element1, element2: IwbElement;
  path1, path2: string;
begin
  if Assigned(e) then begin
    element1 := ElementByPath(e, 'EDID');
    element2 := ElementByPath(e, 'FULL');
    if Assigned(element1) and Assigned(element2) then begin
      path1 := Path(element1);
      path2 := Path(element2);
      AddMessage(Format('Comparing paths: %s vs %s', [path1, path2]));
      if path1 = path2 then
        AddMessage('  Same path component')
      else
        AddMessage('  Different path components');
    end;
  end;
end;
```

## See Also

- [FullPath](IwbElement_FullPath.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)
- [ElementAssign](IwbElement_ElementAssign.md)


