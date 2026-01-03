# ElementByName

## Syntax

```pascal
function ElementByName(AContainer: IwbContainer; AName: string): IwbElement;
```

## Description

Returns an element by its name from the container.

## Examples

```pascal
var
  element: IwbElement;
begin
  element := ElementByName(container, 'EDID'); // Get element named EDID
end;
```

## See Also

- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)


