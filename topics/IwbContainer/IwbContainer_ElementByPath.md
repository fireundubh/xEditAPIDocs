# ElementByPath

## Syntax

```pascal
function ElementByPath(AContainer: IwbContainer; APath: string): IwbElement;
```

## Description

Returns an element by its path from the container. The path is a string representing the hierarchical location of the element.

## Examples

```pascal
var
  element: IwbElement;
begin
  element := ElementByPath(container, 'Model\MODL'); // Get MODL element under Model
end;
```

## See Also

- [ElementByName](IwbContainer_ElementByName.md)
- [ElementExists](IwbContainer_ElementExists.md)
