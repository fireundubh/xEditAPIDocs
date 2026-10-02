# TdfElement.Count

## Syntax

```pascal
property Count: Integer;
```

Access via: `element.Count`

## Description

Gets or sets the number of child elements contained in this element.

The Count property is relevant for container elements (arrays and structures). For variable-length arrays, Count is the number of items and can be written to add or remove entries. A fixed-length array (definition Size greater than 0) ignores writes to Count. For structures, Count returns the number of defined child fields, and writing it raises an exception.

For value elements (integers, floats, bytes), Count is not applicable and returns 0.

Setting Count on an array will create or destroy elements to match the specified count. Elements are created using the array's element definition, and removed elements are properly destroyed.

This property is read-write for variable-length arrays, ignored when written on fixed-length arrays, read-only for structures, and irrelevant for values.

## Parameters

This property has no parameters.

## Returns

Returns the number of child elements as an integer.

## Example

```pascal
var
    arrayElement, child: TdfElement;
    i, childCount: Integer;
begin
    childCount := arrayElement.Count;
    AddMessage('Array has ' + IntToStr(childCount) + ' elements');

    arrayElement.Count := 10;

    for i := 0 to arrayElement.Count - 1 do begin
        child := arrayElement.Items[i];
        AddMessage('Child ' + IntToStr(i) + ': ' + child.Name);
    end;
end;
```

## See Also

- [TdfElement.Add](TdfElement_Add.md)
- [TdfElement.Delete](TdfElement_Delete.md)
- [TdfElement.Items](TdfElement_Items.md)
- [TdfElement.IndexOf](TdfElement_IndexOf.md)
