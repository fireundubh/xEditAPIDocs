# ElementBySignature

## Syntax

```pascal
function ElementBySignature(AContainer: IwbContainer; ASignature: string): IwbElement;
```

## Description

Returns an element by its signature (record type) from the container. The signature is typically a 4-character identifier.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search for the element |
| ASignature | string | The 4-character signature of the element to retrieve |

## Returns

Returns the element with the specified signature as an IwbElement interface.

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


