# IfThen

## Syntax

```pascal
function IfThen(AValue: boolean; ATrue: string; AFalse: string): string;
```

## Description

Returns `ATrue` when `AValue` is `True` and `AFalse` when `AValue` is `False`

Although similar to a ternary expression, both `ATrue` and `AFalse` will be evaluated.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | boolean | The boolean condition to evaluate |
| ATrue | string | The string to return if the condition is True |
| AFalse | string | The string to return if the condition is False |

## Returns

Returns `ATrue` if `AValue` is True, otherwise returns `AFalse`.

## Example

```pascal
function BoolToStr(AValue: boolean): string;
begin
	Result := IfThen(AValue, 'True', 'False');
end;
```

