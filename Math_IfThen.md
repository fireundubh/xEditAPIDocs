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

## Example

```pascal
bSwitch := True;
i := IfThen(bSwitch, 1, 0) + IfThen(not bSwitch, 1, 0);
AddMessage(IntToStr(i));  // Output: 1
```
