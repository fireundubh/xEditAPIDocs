# Remove

## Syntax

```pascal
procedure Remove(AElement: IwbElement);
```

## Description

Removes the element from its parent container.

This function calls the element's Remove method, which detaches it from its parent container and marks it for deletion. The element is removed from memory immediately, but the change is not persisted to disk until the file is saved. This operation is irreversible once the file is saved.

Use with caution. Removing critical elements may corrupt the record structure or make the file invalid.

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


