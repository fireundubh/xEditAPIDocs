# TdfElement.Root

## Syntax

```pascal
function Root: TdfElement;
```

## Description

Returns the topmost element in the hierarchy that contains this element.

The Root property traverses up the parent chain until it reaches the element that has no parent, which is the root of the element tree. For a complete binary file (like a NIF, BGSM, or DDS file), the root element typically represents the entire file structure.

Understanding the root is useful when you need to access file-level properties or perform operations that require context from the entire file structure.

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the root TdfElement. If the current element is already the root, returns itself.

## Example

```pascal
var
    element: TdfElement;
    rootElement: TdfElement;
begin
    rootElement := element.Root;
    AddMessage('Root element name: ' + rootElement.Name);
end;
```

## See Also

- [TdfElement.Parent](TdfElement_Parent.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.ElementByPath](TdfElement_ElementByPath.md)
