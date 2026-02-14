# IndexOf

## Syntax

```pascal
function IndexOf(AContainer: IwbContainer; AElement: IwbElement): integer;
```

## Description

Returns the index of the specified element in the container. Returns `-1` if the element is not found.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| AElement | IwbElement | The element to find the index of |

## Returns

Returns the zero-based index of the element, or -1 if not found.

## Examples

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


