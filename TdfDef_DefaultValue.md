# TdfDef.DefaultValue

## Syntax

```pascal
property DefaultValue: Integer;
```

Access via: `def.DefaultValue`

## Description

Returns the same integer as DefaultDataSize.

The script property does not return the definition's default string. Reading it yields the default data size in bytes. To see the string default applied to an element, call SetToDefault and read EditValue.

## Parameters

This property has no parameters.

## Returns

Returns the default data size in bytes as an integer, the same value as DefaultDataSize.

## Example

```pascal
var
    def: TdfDef;
    dataSize: Integer;
begin
    dataSize := def.DefaultValue;
    AddMessage('Default data size: ' + IntToStr(dataSize));
end;
```

## See Also

- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
