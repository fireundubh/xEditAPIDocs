# IndexOf

## Syntax

```pascal
function IndexOf(AContainer: IwbContainer; AElement: IwbElement): integer;
```

## Description

Searches for an element within the container and returns its zero-based index position.

This function calls the container's IndexOf method with the element to search for. Returns the index (0 to ElementCount-1) if found, or -1 if the element is not a child of this container. Useful for determining element position before operations like MoveUp/MoveDown, or for checking container membership. The search is by element identity (same instance), not by value comparison.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| AElement | IwbElement | The element to find the index of |

## Returns

Returns the zero-based index of the element, or -1 if not found.

## Example

```pascal
var
  index: integer;
begin
  index := IndexOf(container, element);
  if index >= 0 then
    AddMessage('Element found at index ' + IntToStr(index));
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementExists](IwbContainer_ElementExists.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [ElementCount](IwbContainer_ElementCount.md)


