# ElementByIndex

## Syntax

```pascal
function ElementByIndex(AContainer: IwbContainer; AIndex: integer): IwbElement;
```

## Description

Returns the element at the specified zero-based index within the container.

This function accesses the Elements property by index, which provides direct array-style access to child elements. Index 0 returns the first element, index 1 the second, and so on. Returns nil if the index is out of bounds (negative or >= ElementCount). No exception is raised for invalid indices.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the element from |
| AIndex | integer | The zero-based index of the element to retrieve |

## Returns

Returns the element at the specified index as an IwbElement interface.

## Example

```pascal
var
  element: IwbElement;
begin
  element := ElementByIndex(container, 0); // Get first element
end;
```

## See Also

- [ElementCount](IwbContainer_ElementCount.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [IndexOf](IwbContainer_IndexOf.md)
- [LastElement](IwbContainer_LastElement.md)


