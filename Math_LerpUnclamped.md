# LerpUnclamped

## Syntax

```pascal
function LerpUnclamped(A, B, AValue: Double): Double;
```

## Description

Linearly interpolates between `A` and `B` by the factor `AValue`.

Unlike [Lerp](Math_Lerp.md), `AValue` is not clamped.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| A | Double | The start value for interpolation |
| B | Double | The end value for interpolation |
| AValue | Double | The interpolation factor (not clamped) |

## Returns

Returns the interpolated value between A and B.

## Example

```pascal
f := LerpUnclamped(10, 20, 1.5);
AddMessage(FloatToStr(f)); // Output: 25
```

## See Also

- [InverseLerp](Math_InverseLerp.md)
- [Lerp](Math_Lerp.md)
