# TdfElement.Add

## Syntax

```pascal
function Add: TdfElement;
```

Access via: `element.Add`

## Description

Adds a new element to this array and returns the newly created element.

The Add method is primarily used with array elements to append a new entry. The new element is created from the array's element definition and initialized with default values. The array's Count is incremented automatically.

For non-array elements, calling Add raises an exception. Fixed-length arrays (definition Size greater than 0) also raise. Structures have a fixed set of fields and cannot have elements added.

The newly created element is returned so you can immediately set its properties or access its children.

## Parameters

This method has no parameters.

## Returns

Returns the newly created TdfElement that was added to the array.

## Example

```pascal
var
    arrayElement, newItem: TdfElement;
begin
    // Add new element to array
    newItem := arrayElement.Add;
    newItem.EditValue := 'New Item';
    newItem.NativeValues['X'] := 100;
    newItem.NativeValues['Y'] := 200;

    AddMessage('Array now has ' + IntToStr(arrayElement.Count) + ' elements');
end;
```

## See Also

- [TdfElement.Delete](TdfElement_Delete.md)
- [TdfElement.Remove](TdfElement_Remove.md)
- [TdfElement.Count](TdfElement_Count.md)
- [TdfElement.Items](TdfElement_Items.md)
