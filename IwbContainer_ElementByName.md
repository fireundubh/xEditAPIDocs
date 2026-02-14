# ElementByName

## Syntax

```pascal
function ElementByName(AContainer: IwbContainer; AName: string): IwbElement;
```

## Description

Returns an element by its name from the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search for the element |
| AName | string | The name of the element to retrieve |

## Returns

Returns the element with the specified name as an IwbElement interface.

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


