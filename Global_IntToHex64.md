# IntToHex64

## Syntax

```pascal
function IntToHex64(AValue: Int64; ADigits: integer): string;
```

## Description

Returns a hexadecimal representation of `AValue` at least `ADigits` wide

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | Int64 | The 64-bit integer value to convert to hexadecimal |
| ADigits | integer | The minimum width of the hexadecimal string output |

## Returns

Returns a hexadecimal string representation of the value.

## Example

```pascal
s := InputBox('Enter', 'New starting FormID', IntToHex64(OldFormID, 8));

if s = '' then
	Exit;

NewFormID := StrToInt64('$' + s);
```

## See Also

- [IntToHex - System.SysUtils](http://docwiki.embarcadero.com/Libraries/Sydney/en/System.SysUtils.IntToHex)


