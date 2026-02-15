# dfFloatToStr

## Syntax

```pascal
function dfFloatToStr(Value: Double): string;
```

## Description

Converts a floating-point value to a string representation using the data format display settings.

This function formats float values according to the precision configured in xEdit's data format system (controlled by `dfFloatDecimalDigits`). It ensures consistent formatting of floating-point numbers when working with binary file formats like NIF, BGSM, and other data format files.

Unlike Pascal's standard `FloatToStr`, this function uses the data format system's specific formatting rules, which may include fixed precision and locale-independent decimal separators.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Value | Double | The floating-point value to convert to a string |

## Returns

Returns a string representation of the floating-point value formatted according to data format display settings.

## Example

```pascal
var
  floatValue: Double;
  strValue: string;
begin
  floatValue := 123.456789;
  strValue := dfFloatToStr(floatValue);
  AddMessage('Formatted value: ' + strValue);
  // Output depends on dfFloatDecimalDigits setting
end;
```

## See Also

- [dfStrToFloat](Global_dfStrToFloat.md)
- [dfFloatDecimalDigits](Global_dfFloatDecimalDigits.md)
