# IfThen

## Syntax

```pascal
function IfThen(AValue: boolean; ATrue: string; AFalse: string): string;
```

## Description

Returns `ATrue` when `AValue` is `True` and `AFalse` when `AValue` is `False`

Although similar to a ternary expression, both `ATrue` and `AFalse` will be evaluated.

## Example

```pascal
function BoolToStr(AValue: boolean): string;
begin
	Result := IfThen(AValue, 'True', 'False');
end;
```

