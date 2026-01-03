# Remove

## Syntax

```pascal
procedure Remove(AElement: IwbElement);
```

## Description

Removes the element from its file. This operation permanently removes the element from its containing file.

Use with caution as this operation cannot be undone.

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


