# TdfElement.BeginUpdate

## Syntax

```pascal
procedure BeginUpdate;
```

Access via: `element.BeginUpdate`

## Description

Begins an update. Value and text callbacks on this element are skipped until EndUpdate.

BeginUpdate sets an updating flag. While that flag is set, the element's value and text callbacks are not invoked. EndUpdate clears the flag. The calls are not counted: one EndUpdate clears the flag even if BeginUpdate ran more than once.

Always pair BeginUpdate with EndUpdate in a try-finally block so the flag is cleared if an exception occurs.

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
        // Make multiple changes efficiently
        for i := 0 to Pred(element.Count) do begin
            child := element[i];
            child.NativeValue := i * 100;
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
