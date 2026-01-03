# RemoveByIndex

## Syntax

```pascal
function RemoveByIndex(AContainer: IwbContainer; AIndex: integer; AMarkModified: boolean): IwbElement;
```

## Description

Removes and returns the element at the specified index in the container.

## Examples

```pascal
var
  removed: IwbElement;
begin
  removed := RemoveByIndex(container, 0); // Remove first element
end;
```

## See Also

- [RemoveElement](IwbContainer_RemoveElement.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)


