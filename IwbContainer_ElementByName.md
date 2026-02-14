# ElementByName

## Syntax

```pascal
function ElementByName(AContainer: IwbContainer; AName: string): IwbElement;
```

## Description

Searches the container for a child element with the specified name.

This function accesses the ElementByName property, which searches for an element whose Name property matches the provided string. The search is typically case-sensitive and looks at the element's definition name (e.g., "EDID", "DATA"). Returns nil if no element with that name exists in the container. For nested paths, use ElementByPath instead.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search for the element |
| AName | string | The name of the element to retrieve |

## Returns

Returns the element with the specified name as an IwbElement interface.

## Example

```pascal
var
  element: IwbElement;
begin
  element := ElementByName(container, 'EDID'); // Get element named EDID
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [ElementExists](IwbContainer_ElementExists.md)
- [IndexOf](IwbContainer_IndexOf.md)


