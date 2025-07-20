# InsertElement

## Syntax

```pascal
procedure InsertElement(AContainer: IwbContainer; AIndex: Integer; AElement: IwbElement);
```

## Description

Inserts a new element at the specified index position in the container.

This procedure creates a new element with the given signature and inserts it at the specified index. All existing elements at and after the index are shifted right.

## Examples

```pascal
var
  container: IwbContainer;
begin
  InsertElement(container, 0, 'EDID'); // Insert at beginning
end
```

## See Also

- [AddElement](IwbContainer_AddElement.md)
