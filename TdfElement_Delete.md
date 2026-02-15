# TdfElement.Delete

## Syntax

```pascal
procedure Delete(Index: Integer);
```

## Description

Deletes the child element at the specified index from this container.

The Delete method removes a child element at the given zero-based index. The element is properly destroyed and freed from memory. For arrays, this decrements the Count and shifts subsequent elements down by one position.

For structure elements, Delete may raise an exception as structures typically have a fixed set of fields that cannot be removed. Use this method primarily with array elements.

The index must be valid (0 to Count-1), or an exception will be raised.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index of the child element to delete |

## Returns

This method does not return a value.

## Example

```pascal
var
    arrayElement: TdfElement;
begin
    // Delete element at index 5
    arrayElement.Delete(5);

    // Delete first element
    arrayElement.Delete(0);

    // Delete last element
    arrayElement.Delete(arrayElement.Count - 1);

    AddMessage('Array now has ' + IntToStr(arrayElement.Count) + ' elements');
end;
```

## See Also

- [TdfElement.Remove](TdfElement_Remove.md)
- [TdfElement.Add](TdfElement_Add.md)
- [TdfElement.Count](TdfElement_Count.md)
- [TdfElement.Items](TdfElement_Items.md)
