# Add

## Syntax

```pascal
function Add(AContainer: IwbContainer; ANameOrSignature: string; ASilent: boolean): IwbElement;
```

## Description

Creates and adds a new child element to the container by name or signature.

This function calls the container's Add method, which creates a new element based on the provided name or signature string and appends it to the container. The ASilent parameter controls whether change notifications are suppressed. Returns the newly created IwbElement. The element type created depends on the container's definition and the provided name/signature. Commonly used for adding new array elements or optional fields.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to add the element to |
| ANameOrSignature | string | The name or signature of the element to add |
| ASilent | boolean | If true, suppresses notifications during the operation |

## Returns

Returns the newly created element as an IwbElement interface.

## Example

```pascal
var
  newElement: IwbElement;
begin
  newElement := container.Add;
  // Work with the new element
end;
```

## See Also

- [AddElement](IwbContainer_AddElement.md)
- [InsertElement](IwbContainer_InsertElement.md)
- [RemoveElement](IwbContainer_RemoveElement.md)
- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [ElementCount](IwbContainer_ElementCount.md)


