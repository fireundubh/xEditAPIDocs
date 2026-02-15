# TdfElement.Items

## Syntax

```pascal
property Items[Index: Integer]: TdfElement; default;
```

## Description

Returns the child element at the specified index.

The Items property provides array-style access to child elements for container types (structures and arrays). The index is zero-based and must be less than Count. This is the default property, so you can use the element directly with square bracket notation.

For structures, the index corresponds to the order of field definitions. For arrays, the index corresponds to array positions. Accessing an invalid index will raise an exception.

Only enabled elements are included in the indexable collection when accessed through Items.

This property is read-only.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index of the child element to retrieve |

## Returns

Returns the TdfElement at the specified index.

## Example

```pascal
var
    container: TdfElement;
    child: TdfElement;
    i: Integer;
begin
    // Access using Items property explicitly
    child := container.Items[0];

    // Access using default property (bracket notation)
    child := container[1];

    // Iterate all children
    for i := 0 to container.Count - 1 do begin
        child := container[i];
        AddMessage('Child ' + IntToStr(i) + ': ' + child.Name);
    end;
end;
```

## See Also

- [TdfElement.Count](TdfElement_Count.md)
- [TdfElement.Elements](TdfElement_Elements.md)
- [TdfElement.ElementByName](TdfElement_ElementByName.md)
- [TdfElement.IndexOf](TdfElement_IndexOf.md)
