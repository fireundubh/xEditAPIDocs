# AddElement

## Syntax

```pascal
procedure AddElement(AContainer: IwbContainer; AElement: IwbElement);
```

## Description

Adds an existing element instance to the container.

This procedure calls the container's AddElement method, which takes ownership of an already-created element and adds it to the container's child list. The element is typically moved from another location or created separately. This is a lower-level operation compared to Add, which creates new elements. Use when you need to transfer elements between containers or work with pre-constructed elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to add the element to |
| AElement | IwbElement | The element to add to the container |

## Example

```pascal
var
  Container: IwbContainer;
  NewElement: IwbElement;
begin
  NewElement := AddElement(Container, 'EDID');
end
```

## See Also

- [Add](IwbContainer_Add.md)
- [InsertElement](IwbContainer_InsertElement.md)
- [RemoveElement](IwbContainer_RemoveElement.md)


