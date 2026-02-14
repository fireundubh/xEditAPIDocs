# Lerp

## Syntax

```pascal
function Lerp(A, B, AValue: Double): Double;
```

## Description

Linearly interpolates between `A` and `B` by the factor `AValue`.

`AValue` is clamped between 0 and 1.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| A | Double | The start value for interpolation |
| B | Double | The end value for interpolation |
| AValue | Double | The interpolation factor (clamped to 0-1) |

## Returns

Returns the interpolated value between A and B.

## Example

```pascal
f := Lerp(10, 20, 0.5);
AddMessage(FloatToStr(f)); // Output: 15
```

## See Also

- [InverseLerp](Math_InverseLerp.md)
- [LerpUnclamped](Math_LerpUnclamped.md)
