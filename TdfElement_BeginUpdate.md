# TdfElement.BeginUpdate

## Syntax

```pascal
procedure BeginUpdate;
```

## Description

Begins a batch update operation, suspending change notifications and callbacks.

The BeginUpdate method marks the element as being in an update state, which prevents certain callbacks and validations from firing during bulk modifications. This improves performance when making multiple changes and ensures consistency by deferring validation until EndUpdate is called.

BeginUpdate and EndUpdate calls can be nested. The element only exits the update state when the matching EndUpdate is called for the outermost BeginUpdate.

Always pair BeginUpdate with EndUpdate in a try-finally block to ensure the update state is properly cleared even if an exception occurs.

This method has no return value.

## Parameters

This method has no parameters.

## Returns

This method does not return a value.

## Example

```pascal
var
    element: TdfElement;
    i: Integer;
begin
    element.BeginUpdate;
    try
        // Make multiple changes efficiently
        for i := 0 to 99 do begin
            element[i].NativeValue := i * 100;
        end;
    finally
        element.EndUpdate;
    end;
end;
```

## See Also

- [TdfElement.EndUpdate](TdfElement_EndUpdate.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
