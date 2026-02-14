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
var
  pathComponent: string;
begin
  pathComponent := Path(element);
end;
```

## See Also

- [FullPath](IwbElement_FullPath.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)
- [ElementAssign](IwbElement_ElementAssign.md)


