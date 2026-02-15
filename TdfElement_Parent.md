# TdfElement.Parent

## Syntax

```pascal
property Parent: TdfElement;
```

## Description

Gets or sets the parent element that contains this element in the hierarchy.

The Parent property establishes the hierarchical relationship between elements in a binary file structure. Each element (except the root) has a parent that contains it. This parent-child relationship forms a tree structure that mirrors the logical organization of the binary data.

Setting the Parent property allows you to move elements within the tree structure or attach orphaned elements to a new container. However, this should be done carefully as it affects the serialization and path of the element.

This property is read-write.

## Parameters

This property has no parameters.

## Returns

Returns the parent TdfElement, or nil if this is the root element.

## Example

```pascal
var
    element: TdfElement;
    parent: TdfElement;
    newParent: TdfElement;
begin
    // Get parent
    parent := element.Parent;
    if Assigned(parent) then
        AddMessage('Parent name: ' + parent.Name);

    // Set new parent
    element.Parent := newParent;
end;
```

## See Also

- [TdfElement.Root](TdfElement_Root.md)
- [TdfElement.Path](TdfElement_Path.md)
- [TdfElement.Index](TdfElement_Index.md)
- [TdfElement.Count](TdfElement_Count.md)
