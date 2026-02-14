# Remove

## Syntax

```pascal
procedure Remove(AElement: IwbElement);
```

## Description

Removes the element from its file. This operation permanently removes the element from its containing file.

Use with caution as this operation cannot be undone.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to remove from its file |

## Example

```pascal
var
    elementToDelete: IwbElement;
begin
    Remove(elementToDelete);
end;
```

## See Also

- [RemoveByIndex](IwbContainer_RemoveByIndex.md)
- [RemoveElement](IwbContainer_RemoveElement.md)


