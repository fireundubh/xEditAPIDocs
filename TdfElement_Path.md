# TdfElement.Path

## Syntax

```pascal
function Path: string;
```

Access via: `element.Path`

## Description

Returns this element's path. The root name is not included except when this element is the root.

Path builds a backslash-separated path from this element toward the root, but it omits the root element's name. The root element's own path is just its name. A direct child of the root has a path equal to that child's name. A deeper element joins ancestor names, such as `Header\Version` when `Header` is not the root. Each segment is the Name property. An array child is `DefName #index`, not `[index]` bracket syntax.

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
