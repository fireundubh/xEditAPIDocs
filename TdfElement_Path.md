# TdfElement.Path

## Syntax

```pascal
function Path: string;
```

## Description

Returns the full hierarchical path from the root element to this element.

The Path property constructs a string that represents the complete navigation path through the element tree from the root to the current element. Each level in the hierarchy is separated by a backslash (\). This is analogous to a file system path and is useful for identifying the location of an element within a complex binary structure.

For example, in a NIF file, a path might look like: "NiNode\Children\[0]\NiTriShape\Data"

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the full path as a string with backslash separators.

## Example

```pascal
var
    element: TdfElement;
    fullPath: string;
begin
    fullPath := element.Path;
    AddMessage('Element path: ' + fullPath);
end;
```

## See Also

- [TdfElement.Name](TdfElement_Name.md)
- [TdfElement.Parent](TdfElement_Parent.md)
- [TdfElement.Root](TdfElement_Root.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
