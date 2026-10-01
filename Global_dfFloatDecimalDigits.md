# dfFloatDecimalDigits

## Syntax

```pascal
function dfFloatDecimalDigits: integer;
```

Assign it as well. The assignment takes an integer and returns nothing.

```pascal
dfFloatDecimalDigits := 6;
```

## Description

Reads or sets how many digits follow the decimal point when data-format code formats a float. The initial value is 6.

Before the assignment is stored, the host checks the current value. If that current value is not greater than 0, the assignment raises `dfFloatDecimalDigits must be greater than 0`. The new value is not checked.

## Parameters

The function takes no parameters. The assignment takes the new digit count.

## Returns

The function returns the current digit count. The assignment returns nothing.

## Example

```pascal
begin
  AddMessage(IntToStr(dfFloatDecimalDigits));
  dfFloatDecimalDigits := 4;
end;
```

## See Also

- [wbSettings](Global_wbSettings.md)
