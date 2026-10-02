# TdfDef.Size

## Syntax

```pascal
property Size: Integer;
```

Access via: `def.Size`

## Description

Returns the size constraint stored on the definition. This property is read-only from scripts.

Zero means DefaultDataSize comes from the data type (0 for structs, arrays, and unsized bytes or chars). On an array, a positive Size is a fixed element count: Add and Delete raise, and writing Count has no effect. On bytes or chars, a positive Size is the byte length used as DefaultDataSize. When Size is negative, TdfDef.DefaultDataSize returns -Size (bytes and chars inherit that). On an array, bytes, or chars that width is a count prefix, not the payload length: only a prefix of 1, 2, or 4 bytes loads a stored count, and any other width uses a count of 0. A merge's DefaultDataSize ignores Size.

## Parameters

This property has no parameters.

## Returns

Returns the stored size as an integer. The meaning of a non-zero value depends on the definition, as described above.

## Example

```pascal
var
    def: TdfDef;
    fixedSize: Integer;
begin
    fixedSize := def.Size;
    AddMessage('Size: ' + IntToStr(fixedSize));
end;
```

## See Also

- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
- [TdfElement.Count](TdfElement_Count.md)
- [TdfDef.Name](TdfDef_Name.md)
