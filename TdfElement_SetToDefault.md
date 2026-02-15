# TdfElement.SetToDefault

## Syntax

```pascal
procedure SetToDefault;
```

## Description

Resets this element's value to the default specified in its definition.

The SetToDefault method restores the element to its initial state by applying the default value from its TdfDef. For primitive types (integers, floats), this sets the value to the definition's DefaultValue. For structures and arrays, this may recursively reset all child elements to their defaults.

This is useful for initializing new elements or clearing modifications back to a known state.

The behavior depends on the element's data type:
- Value types: Set to DefaultValue from definition
- Arrays: May clear to empty or set to default count
- Structures: Recursively reset child fields

This method has no return value.

## Parameters

This method has no parameters.

## Returns

This method does not return a value.

## Example

```pascal
var
    element: TdfElement;
begin
    // Modify element
    element.NativeValue := 999;
    AddMessage('Modified value: ' + element.EditValue);

    // Reset to default
    element.SetToDefault;
    AddMessage('Default value: ' + element.EditValue);

    // For structures, resets all fields
    structElement.SetToDefault;
end;
```

## See Also

- [TdfDef.DefaultValue](TdfDef_DefaultValue.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
- [TdfElement.Assign](TdfElement_Assign.md)
