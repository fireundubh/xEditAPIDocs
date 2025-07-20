# FullPath

## Syntax

```pascal
function FullPath(AElement: IwbElement): string;
```

## Description

Returns the complete path to the element, including its containing file.

This function provides the full hierarchical path to the element, starting from its containing file and including all parent elements. This is different from Path which returns only a single path component.

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
- [PathName](IwbElement_PathName.md)
