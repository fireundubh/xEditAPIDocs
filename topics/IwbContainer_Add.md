# Add

## Syntax

```pascal
function Add(AContainer: IwbContainer; ANameOrSignature: string; ASilent: boolean): IwbElement;
```

## Description

Adds and returns a new child element to the container.

Creates a new element as a child of this container and returns the newly created element. The exact type of element created depends on the container type.

## Examples

```pascal
var
  newElement: IwbElement;
begin
  newElement := container.Add;
  // Work with the new element
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)
- [RemoveElement](IwbContainer_RemoveElement.md)


