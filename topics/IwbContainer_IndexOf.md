# IndexOf

## Syntax

```pascal
function IndexOf(AContainer: IwbContainer; AElement: IwbElement): integer;
```

## Description

Returns the index of the specified element in the container. Returns `-1` if the element is not found.

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


