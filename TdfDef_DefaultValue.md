# TdfDef.DefaultValue

## Syntax

```pascal
property DefaultValue: string;
```

## Description

Returns the default value that elements created from this definition will be initialized with.

The DefaultValue property specifies what value new elements should have when created or when reset to defaults using SetToDefault. This is stored as a string representation but will be converted to the appropriate native type when applied to elements. For example, a float definition might have "0.0" as its default value, while an integer might have "0" or "-1".

This property is read-only from script context and is configured when the definition is created.

## Parameters

This property has no parameters.

## Returns

Returns the default value as a string. May be an empty string if no default is specified.

## Example

```pascal
var
    def: TdfDef;
    defaultVal: string;
begin
    defaultVal := def.DefaultValue;
    AddMessage('Default value: ' + defaultVal);
end;
```

## See Also

- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
- [TdfDef.DefaultDataSize](TdfDef_DefaultDataSize.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
