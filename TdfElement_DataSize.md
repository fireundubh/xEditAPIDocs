# TdfElement.DataSize

## Syntax

```pascal
function DataSize: Integer;
```

## Description

Returns the actual size in bytes that this element occupies when serialized to binary format.

The DataSize property calculates the current binary size of the element based on its data type, content, and children. Unlike TdfDef.DefaultDataSize which returns a theoretical default size, this property returns the actual current size accounting for variable-length data, array counts, and optional fields.

For primitive types, this returns the fixed size (e.g., 4 for dtU32). For structures and arrays, this is the sum of all enabled child element sizes. For variable-length types like dtBytes or dtChars, this reflects the actual data length.

This property is read-only.

## Parameters

This property has no parameters.

## Returns

Returns the binary size in bytes as an integer.

## Example

```pascal
var
    element: TdfElement;
    size: Integer;
begin
    size := element.DataSize;
    AddMessage('Element occupies ' + IntToStr(size) + ' bytes');
end;
```

## See Also

- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfDef.Size](TdfDef_Size.md)
- [TdfElement.SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement.LoadFromData](TdfElement_LoadFromData.md)
