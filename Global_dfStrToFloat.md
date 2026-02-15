# dfStrToFloat

## Syntax

```pascal
function dfStrToFloat(Value: string): Double;
```

## Description

Converts a string representation to a floating-point value using the data format parsing rules.

This function parses string values according to the data format system's rules, which use locale-independent parsing and handle the precision settings configured in xEdit. It's the inverse operation of `dfFloatToStr` and ensures consistent parsing when reading or editing binary file format data.

Unlike Pascal's standard `StrToFloat`, this function uses data format-specific parsing rules that may handle edge cases differently, particularly for very small or very large values, and uses consistent decimal separator handling regardless of system locale.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Value | string | The string representation of a floating-point value |

## Returns

Returns a Double representing the parsed floating-point value.

## Example

```pascal
var
  strValue: string;
  floatValue: Double;
begin
  strValue := '123.456789';
  floatValue := dfStrToFloat(strValue);
  AddMessage(Format('Parsed value: %f', [floatValue]));
end;
```

## See Also

- [dfFloatToStr](Global_dfFloatToStr.md)
- [dfFloatDecimalDigits](Global_dfFloatDecimalDigits.md)
