# TdfElement.Remove

## Syntax

```pascal
procedure Remove;
```

## Description

Removes this element from its parent container.

The Remove method deletes this element from its parent's child collection. This is equivalent to calling Delete on the parent with this element's index. The element is properly destroyed and freed from memory.

After calling Remove, the element reference becomes invalid and should not be used. Any further access to the removed element will cause an error.

For array elements, this decrements the array's Count. For structure elements, Remove may raise an exception as structures typically have a fixed set of fields that cannot be removed.

This method has no return value.

## Parameters

This method has no parameters.

## Returns

This method does not return a value.

## Example

```pascal
var
    arrayElement: TdfElement;
    itemToRemove: TdfElement;
begin
    itemToRemove := arrayElement[5];

    // Remove the element
    itemToRemove.Remove;
    // itemToRemove is now invalid and should not be used

    AddMessage('Array now has ' + IntToStr(arrayElement.Count) + ' elements');
end;
```

## See Also

- [TdfElement.Delete](TdfElement_Delete.md)
- [TdfElement.Add](TdfElement_Add.md)
- [TdfElement.Index](TdfElement_Index.md)
- [TdfElement.Parent](TdfElement_Parent.md)
