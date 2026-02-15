# TdfElement.Assign

## Syntax

```pascal
procedure Assign(const aElement: TdfElement);
```

## Description

Copies all data from another element into this element.

The Assign method performs a deep copy of data from the source element to this element. Both elements should have compatible definitions (same structure and data types), though exact definition identity is not always required.

For value types, this copies the binary data. For containers (structures and arrays), this recursively copies all child elements, creating new element instances as needed. The Count of array elements is adjusted to match the source.

This is useful for duplicating elements, creating backups before modifications, or transferring data between similar structures.

If the elements have incompatible structures, the behavior depends on the specific element types - some assignments may partially succeed or raise exceptions.

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
    // Copy data from source to destination
    destination.Assign(source);

    // Verify copy
    AddMessage('Source value: ' + source.EditValue);
    AddMessage('Destination value: ' + destination.EditValue);

    // Useful for backing up before modification
    backup := TdfElement.Create(element.Def, nil);
    backup.Assign(element);
    // Modify element...
    // Restore if needed:
    element.Assign(backup);
end;
```

## See Also

- [TdfElement.SetToDefault](TdfElement_SetToDefault.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.FromJSON](TdfElement_FromJSON.md)
- [TdfElement.ToJSON](TdfElement_ToJSON.md)
