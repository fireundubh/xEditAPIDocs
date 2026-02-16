# TdfElement.EditValue

## Syntax

```pascal
property EditValue: string;
```

## Description

Gets or sets the element's value as a human-readable string.

The EditValue property provides access to the element's data in a formatted, user-friendly string representation. For integers, this is the decimal string representation. For floats, this includes decimal formatting. For enums and flags, this may include mapped names. For bytes/chars, this is the string interpretation.

EditValue handles the conversion between string representation and the underlying binary data automatically. When setting EditValue, the string is parsed according to the element's data type. Invalid strings that cannot be parsed will typically result in the value being set to 0 or the default value.

This differs from NativeValue which returns data in its native Variant type. Use EditValue for display purposes and user input, and NativeValue for calculations.

Use EditValue when you already have a reference to the specific element you want to read or write. If you need to access a child element's value by path, use EditValues instead — it combines path navigation and value access in a single call, avoiding the need to chain calls like `element.ElementByPath('Name').EditValue` which is not supported by the scripting engine.

This property is read-write.

## Parameters

This property has no parameters.

## Returns

Returns the element's value as a formatted string.

## Example

```pascal
var
    element: TdfElement;
    displayText: string;
begin
    // Read edit value
    displayText := element.EditValue;
    AddMessage('Display value: ' + displayText);

    // Set edit value
    element.EditValue := '123';

    // For floats
    element.EditValue := '3.14159';

    // For enums (if mapped)
    element.EditValue := 'ALPHA_BLEND';
end;
```

## See Also

- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.EditValues](TdfElement_EditValues.md)
- [TdfElement.ToText](TdfElement_ToText.md)
- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
