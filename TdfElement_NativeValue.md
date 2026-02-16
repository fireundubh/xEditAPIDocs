# TdfElement.NativeValue

## Syntax

```pascal
property NativeValue: Variant;
```

## Description

Gets or sets the element's value in its native binary representation.

The NativeValue property provides direct access to the element's data as it exists in memory, using appropriate variant types. For integer types, this returns Integer or Int64 values. For float types, this returns Double values. For bytes/chars, this returns byte arrays or strings. For structures and arrays, behavior depends on the specific definition.

This differs from EditValue which always returns a human-readable string representation. NativeValue is preferred when performing calculations or comparisons, while EditValue is better for display and user input.

Use NativeValue when you already have a reference to the specific element you want to read or write. If you need to access a child element's value by path, use NativeValues instead — it combines path navigation and value access in a single call, avoiding the need to chain calls like `element.ElementByPath('Name').NativeValue` which is not supported by the scripting engine.

For container elements (structs/arrays), the behavior of NativeValue depends on custom callbacks defined in the element's definition.

This property is read-write.

## Parameters

This property has no parameters.

## Returns

Returns the element's value as a Variant in its native type.

## Example

```pascal
var
    element: TdfElement;
    intValue: Integer;
    floatValue: Double;
begin
    // Read native value
    intValue := element.NativeValue;
    AddMessage('Value: ' + IntToStr(intValue));

    // Set native value
    element.NativeValue := 42;

    // For floats
    floatValue := element.NativeValue;
    element.NativeValue := 3.14159;
end;
```

## See Also

- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.NativeValues](TdfElement_NativeValues.md)
- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
- [TdfDef.DefaultValue](TdfDef_DefaultValue.md)
