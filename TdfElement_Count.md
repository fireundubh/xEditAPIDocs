# TdfElement.Count

## Syntax

```pascal
property Count: Integer;
```

## Description

Gets or sets the number of child elements contained in this element.

The Count property is relevant for container elements (arrays and structures). For array elements, Count indicates how many items are in the array and can be modified to add or remove array entries. For structures, Count returns the number of defined child fields and is typically read-only (attempting to set it may raise an exception).

For value elements (integers, floats, bytes), Count is not applicable and returns 0.

Setting Count on an array will create or destroy elements to match the specified count. Elements are created using the array's element definition, and removed elements are properly destroyed.

This property is read-write for arrays, read-only for structures, and irrelevant for values.

## Parameters

This property has no parameters.

## Returns

Returns the number of child elements as an integer.

## Example

```pascal
var
    arrayElement: TdfElement;
    i, childCount: Integer;
begin
    // Get current count
    childCount := arrayElement.Count;
    AddMessage('Array has ' + IntToStr(childCount) + ' elements');

    // Resize array
    arrayElement.Count := 10;

    // Iterate children
    for i := 0 to arrayElement.Count - 1 do
        AddMessage('Child ' + IntToStr(i) + ': ' + arrayElement.Items[i].Name);
end;
```

## See Also

- [TdfElement.Add](TdfElement_Add.md)
- [TdfElement.Delete](TdfElement_Delete.md)
- [TdfElement.Items](TdfElement_Items.md)
- [TdfElement.IndexOf](TdfElement_IndexOf.md)
