# RemoveByIndex

## Syntax

```pascal
function RemoveByIndex(AContainer: IwbContainer; AIndex: integer; AMarkModified: boolean): IwbElement;
```

## Description

Removes and returns the element at the specified index in the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to remove the element from |
| AIndex | integer | The zero-based index of the element to remove |
| AMarkModified | boolean | If true, marks the container as modified |

## Returns

Returns the removed element as an IwbElement interface.

## Examples

```pascal
var
  removed: IwbElement;
begin
  removed := RemoveByIndex(container, 0); // Remove first element
end;
```

## See Also

- [RemoveElement](IwbContainer_RemoveElement.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)


