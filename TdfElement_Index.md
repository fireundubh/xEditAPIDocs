# TdfElement.Index

## Syntax

```pascal
function Index: Integer;
```

## Description

Returns the position of this element within its parent's child collection.

The Index property provides the zero-based index indicating where this element appears in its parent's list of children. This is particularly useful when working with array elements or when you need to determine the relative position of a struct field.

For the root element or elements without a parent, this returns -1.

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the zero-based index as an integer, or -1 if the element has no parent.

## Example

```pascal
var
    element: TdfElement;
    idx: Integer;
begin
    idx := element.Index;
    if idx >= 0 then
        AddMessage('Element is at position ' + IntToStr(idx))
    else
        AddMessage('Element has no parent (is root)');
end;
```

## See Also

- [TdfElement.Parent](TdfElement_Parent.md)
- [TdfElement.IndexOf](TdfElement_IndexOf.md)
- [TdfElement.Move](TdfElement_Move.md)
- [TdfElement.Items](TdfElement_Items.md)
