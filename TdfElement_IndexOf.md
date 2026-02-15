# TdfElement.IndexOf

## Syntax

```pascal
function IndexOf(aElement: TdfElement): Integer;
```

## Description

Returns the index of the specified child element within this container.

The IndexOf method searches this element's children for the given element and returns its zero-based position. This is useful for determining the relative position of a child element or checking if an element is a direct child of this container.

If the element is not found among the direct children, returns -1. This method only searches immediate children, not all descendants.

For non-container elements (values), this always returns -1.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aElement | TdfElement | The child element to search for |

## Returns

Returns the zero-based index of the element, or -1 if not found.

## Example

```pascal
var
    parent, child: TdfElement;
    idx: Integer;
begin
    idx := parent.IndexOf(child);
    if idx >= 0 then
        AddMessage('Child found at index ' + IntToStr(idx))
    else
        AddMessage('Child not found in parent');
end;
```

## See Also

- [TdfElement.Index](TdfElement_Index.md)
- [TdfElement.Items](TdfElement_Items.md)
- [TdfElement.Count](TdfElement_Count.md)
- [TdfElement.ElementByName](TdfElement_ElementByName.md)
