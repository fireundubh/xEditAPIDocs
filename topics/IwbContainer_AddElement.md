# AddElement

## Syntax

```pascal
procedure AddElement(AContainer: IwbContainer; AElement: IwbElement);
```

## Description

Adds a new element to the specified container using the provided element signature.

This procedure creates and appends a new element to the end of the container. The element signature determines the type of element to create. Returns the newly created element.

## Examples

```pascal
var
  Container: IwbContainer;
  NewElement: IwbElement;
begin
  NewElement := AddElement(Container, 'EDID');
end
```

## See Also

- [InsertElement](IwbContainer_InsertElement.md)


