# TdfDef.DefaultDataSize

## Syntax

```pascal
property DefaultDataSize: Integer;
```

## Description

Returns the default size in bytes that elements created from this definition will occupy in binary data.

The DefaultDataSize property indicates how many bytes an element conforming to this definition typically requires when serialized to binary format. For primitive types (integers, floats), this is a fixed size (e.g., 4 bytes for dtU32, 8 bytes for dtU64). For complex types (structs, arrays), this may be calculated based on child definitions or return 0 if the size is variable.

This property is read-only and calculated based on the definition's data type and structure.

## Parameters

This property has no parameters.

## Returns

Returns the default data size in bytes as an integer. Returns 0 for variable-sized types.

## Example

```pascal
var
    def: TdfDef;
    dataSize: Integer;
begin
    dataSize := def.DefaultDataSize;
    AddMessage('Default size: ' + IntToStr(dataSize) + ' bytes');
end;
```

## See Also

- [TdfDef.Size](TdfDef_Size.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
- [TdfDef.Name](TdfDef_Name.md)
- [TdfDef.DefaultValue](TdfDef_DefaultValue.md)
