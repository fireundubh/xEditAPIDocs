# RemoveElement

## Syntax

```pascal
function RemoveElement(AContainer: IwbContainer; AChild: Variant): IwbElement;
```

## Description

Removes a child element from the container by index, name, or element reference.

This function calls the container's RemoveElement method with flexible input handling. It accepts an integer (removes by index), string (removes by name), or IwbElement (removes specific element instance). Returns the removed element. The element is detached from the container but the reference remains valid until all references are released. Indices and element positions may shift after removal.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to remove the element from |
| AChild | Variant | The element or element name to remove |

## Returns

Returns the removed element as an IwbElement interface.

## Example

```pascal
var
  removed: IwbElement;
begin
  removed := RemoveElement(container, 'Model');
end;
```

## See Also

- [Add](IwbContainer_Add.md)
- [AddElement](IwbContainer_AddElement.md)
- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [Remove](IwbElement_Remove.md)


