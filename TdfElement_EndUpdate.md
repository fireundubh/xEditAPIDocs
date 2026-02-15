# TdfElement.EndUpdate

## Syntax

```pascal
procedure EndUpdate;
```

## Description

Ends a batch update operation, resuming change notifications and callbacks.

The EndUpdate method marks the end of an update batch started with BeginUpdate. Once called (and if this was the outermost BeginUpdate/EndUpdate pair), the element exits the update state and any deferred validations or callbacks can execute.

If BeginUpdate was called multiple times (nested), EndUpdate must be called the same number of times before the element fully exits the update state.

Always call EndUpdate in a finally block to ensure the update state is properly cleared even if an exception occurs during modifications.

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
        // Always call EndUpdate in finally block
        element.EndUpdate;
    end;
end;
```

## See Also

- [TdfElement.BeginUpdate](TdfElement_BeginUpdate.md)
- [TdfElement.NativeValue](TdfElement_NativeValue.md)
- [TdfElement.EditValue](TdfElement_EditValue.md)
