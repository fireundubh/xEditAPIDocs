# IfThen

## Syntax

```pascal
function IfThen(AValue: Boolean; ATrue: Integer; AFalse: Integer): Integer;

function IfThen(AValue: Boolean; ATrue: Single; AFalse: Single): Single;

function IfThen(AValue: Boolean; ATrue: Double; AFalse: Double): Double;

function IfThen(AValue: Boolean; ATrue: Variant; AFalse: Variant): Variant;
```

## Description

Returns `ATrue` when `AValue` is `True` and `AFalse` when `AValue` is `False`.

One three-argument `IfThen` is registered. Integer, single, and double results are used when `ATrue` and `AFalse` have that same type. String results are the same function; see [IfThen](StrUtils_IfThen.md). If `ATrue` and `AFalse` have different types, the selected argument is returned unchanged.

Although similar to a ternary expression, both `ATrue` and `AFalse` will be evaluated.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | Boolean | The boolean condition to evaluate |
| ATrue | Integer, Single, Double, string, or Variant | The value to return if the condition is True. Must be the same type as `AFalse` for the integer, single, double, or string result |
| AFalse | Integer, Single, Double, string, or Variant | The value to return if the condition is False. Required; there is no default |

## Returns

Returns `ATrue` if `AValue` is True, otherwise returns `AFalse`.

## Example

```pascal
var
  bSwitch: Boolean;
  i: Integer;
begin
  bSwitch := True;
  i := IfThen(bSwitch, 1, 0) + IfThen(not bSwitch, 1, 0);
  AddMessage(IntToStr(i));
end;
```

## See Also

- [IfThen](StrUtils_IfThen.md)
