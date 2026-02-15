# TdfDef.Size

## Syntax

```pascal
property Size: Integer;
```

## Description

Returns the fixed size constraint for elements created from this definition, if one has been explicitly set.

The Size property differs from DefaultDataSize in that it represents an explicitly configured size constraint rather than a calculated default. This is primarily used for array definitions where the element count or total byte size is fixed. When Size is set to a non-zero value, it overrides the default size calculation.

For most definitions, this will return 0, indicating that size should be determined dynamically or from DefaultDataSize.

This property is read-only from script context.

## Parameters

This property has no parameters.

## Returns

Returns the fixed size constraint as an integer. Returns 0 if no explicit size constraint is set.

## Example

```pascal
var
    def: TdfDef;
    fixedSize: Integer;
begin
    fixedSize := def.Size;
    if fixedSize > 0 then
        AddMessage('Fixed size: ' + IntToStr(fixedSize))
    else
        AddMessage('Variable size element');
end;
```

## See Also

- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfElement.DataSize](TdfElement_DataSize.md)
- [TdfElement.Count](TdfElement_Count.md)
- [TdfDef.Name](TdfDef_Name.md)
