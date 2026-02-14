# GetContainer

## Syntax

```pascal
function GetContainer(AElement: IwbElement): IwbContainer;
```

## Description

Returns the immediate parent container that holds this element.

This function retrieves the Container property, which provides access to the element's direct parent in the record hierarchy. For a field in a struct, this returns the struct. For a record, this returns the group. Returns nil if the element is at the top level or is invalid. Useful for navigating upward through the element tree.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the container for |

## Returns

Returns the immediate container as an IwbContainer interface.

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
- [GetFile](IwbElement_GetFile.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementByName](IwbContainer_ElementByName.md)


