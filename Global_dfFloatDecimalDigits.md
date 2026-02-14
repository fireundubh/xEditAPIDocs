# dfFloatDecimalDigits

## Syntax

```pascal
function dfFloatDecimalDigits: Integer;
```

## Description

Returns the number of decimal digits to display for floating-point values in the data format display. This setting controls the precision shown for float values throughout xEdit's user interface.

## Parameters

This function takes no parameters.

## Returns

Returns an Integer representing the number of decimal digits used for displaying floating-point values.

## Example

```pascal
var
  precision: Integer;
begin
  precision := dfFloatDecimalDigits;
  AddMessage('Current float display precision: ' + IntToStr(precision) + ' decimal places');
end;
```

## See Also

- [wbSettings](Global_wbSettings.md)
