# ElementBySignature

## Syntax

```pascal
function ElementBySignature(AContainer: IwbContainer; ASignature: string): IwbElement;
```

## Description

Returns an element by its signature (record type) from the container. The signature is typically a 4-character identifier.

## Examples

```pascal
var
  element: IwbElement;
begin
  element := ElementBySignature(container, 'FULL'); // Get FULL record
end;
```

## See Also

- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
