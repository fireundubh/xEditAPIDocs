# ElementByIndex

## Syntax

```pascal
function ElementByIndex(AContainer: IwbContainer; AIndex: integer): IwbElement;
```

## Description

Returns the element at the specified index in the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the element from |
| AIndex | integer | The zero-based index of the element to retrieve |

## Returns

Returns the element at the specified index as an IwbElement interface.

## Examples

```pascal
var
  element: IwbElement;
begin
  element := ElementByIndex(container, 0); // Get first element
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)
- [IndexOf](IwbContainer_IndexOf.md)
- [LastElement](IwbContainer_LastElement.md)


