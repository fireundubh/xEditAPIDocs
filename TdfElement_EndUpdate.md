# TdfElement.EndUpdate

## Syntax

```pascal
procedure EndUpdate;
```

Access via: `element.EndUpdate`

## Description

Ends an update and lets value and text callbacks run again.

EndUpdate clears the updating flag set by BeginUpdate. It is not a nesting counter: one call clears the flag even if BeginUpdate ran more than once. Value and text callbacks run again after the flag is clear.

Always call EndUpdate in a finally block so the flag is cleared if an exception occurs during modifications.

This method has no return value.

## Parameters

This method has no parameters.

## Returns

This method does not return a value.

## Example

```pascal
var
    element, child: TdfElement;
    i: Integer;
begin
    element.BeginUpdate;
    try
        for i := 0 to Pred(element.Count) do begin
            child := element[i];
            child.NativeValue := i * 100;
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
