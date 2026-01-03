# ElementByIndex

## Syntax

```pascal
function ElementByIndex(AContainer: IwbContainer; AIndex: integer): IwbElement;
```

## Description

Returns the element at the specified index in the container.

## Examples

```pascal
var
  element: IwbElement;
begin
  element := ElementByIndex(container, 0); // Get first element
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)
- [IndexOf](IwbContainer_IndexOf.md)
- [LastElement](IwbContainer_LastElement.md)


