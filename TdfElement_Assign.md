# TdfElement.Assign

## Syntax

```pascal
procedure Assign(const aElement: TdfElement);
```

Access via: `element.Assign(source)`

## Description

Copies all data from another element into this element.

The Assign method performs a deep copy of data from the source element to this element. Both elements should have compatible definitions (same structure and data types), though exact definition identity is not always required.

For value types, this copies the binary data. For containers (structures and arrays), this recursively copies all child elements, creating new element instances as needed. The Count of array elements is adjusted to match the source.

This is useful for duplicating elements, creating backups before modifications, or transferring data between similar structures.

Assign does not raise for a type mismatch. It returns without copying when the source is nil, this element is disabled, or the source class does not match: a struct copies only from a struct, an array only from an array, and a value or union only from a value or a union. A value copies bytes only when the source is a value with the same data type and data size; otherwise a value or union copies EditValue.

This method has no return value.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aElement | TdfElement | The source element to copy data from |

## Returns

This method does not return a value.

## Example

```pascal
var
    source, destination: TdfElement;
begin
    destination.Assign(source);
    AddMessage('Source value: ' + source.EditValue);
    AddMessage('Destination value: ' + destination.EditValue);
end;
```

## See Also

- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.FromJSON](TdfElement_FromJSON.md)
- [TdfElement.ToJSON](TdfElement_ToJSON.md)
