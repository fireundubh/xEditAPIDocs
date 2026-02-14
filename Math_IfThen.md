# IfThen

## Syntax

```pascal
function IfThen(AValue: boolean; ATrue: integer; AFalse: integer): integer;

function IfThen(AValue: boolean; ATrue: single; AFalse: single): single;

function IfThen(AValue: boolean; ATrue: double; AFalse: double): double;

function IfThen(AValue: boolean; ATrue: Variant; AFalse: Variant): Variant;
```

## Description

Returns `ATrue` when `AValue` is `True` and `AFalse` when `AValue` is `False`

Although similar to a ternary expression, both `ATrue` and `AFalse` will be evaluated.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | boolean | The boolean condition to evaluate |
| ATrue | integer/single/double/Variant | The value to return if the condition is True |
| AFalse | integer/single/double/Variant | The value to return if the condition is False |

## Returns

Returns `ATrue` if `AValue` is True, otherwise returns `AFalse`.

## Example

```pascal
bSwitch := True;
i := IfThen(bSwitch, 1, 0) + IfThen(not bSwitch, 1, 0);
AddMessage(IntToStr(i));  // Output: 1
```
