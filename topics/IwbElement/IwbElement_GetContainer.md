# GetContainer

## Syntax

```pascal
function GetContainer(AElement: IwbElement): IwbContainer;
```

## Description

Retrieves the element's immediate container.

Returns the container element that directly holds the specified element. This is useful for navigating the element hierarchy upwards.

## Example

```pascal
var
  element: IwbElement;
  container: IwbContainer;
begin
  container := GetContainer(element);
  if Assigned(container) then
    // Work with the container
end;
```

## See Also

- [ContainingMainRecord](IwbElement_ContainingMainRecord.md)
