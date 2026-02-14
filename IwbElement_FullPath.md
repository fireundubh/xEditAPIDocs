# FullPath

## Syntax

```pascal
function FullPath(AElement: IwbElement): string;
```

## Description

Returns the complete hierarchical path from the file root to this element.

This function retrieves the FullPath property, which builds the full path string by traversing from the element up through all parent containers to the file. The path uses backslash separators and includes the filename at the start (e.g., "Skyrim.esm\WEAP\[00012345]\EDID"). Useful for logging, debugging, and uniquely identifying elements. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the full path for |

## Returns

Returns the complete hierarchical path as a string.

## Example

```pascal
var
  element: IwbElement;
  fullPath: string;
begin
  fullPath := FullPath(element);
  // Might return something like "Skyrim.esm\WRLD\Tamriel\Cell Data"
end;
```

## See Also

- [Path](IwbElement_Path.md)
- [IndexedPath](IwbElement_IndexedPath.md)
- [PathName](IwbElement_PathName.md)
- [Name](IwbElement_Name.md)


