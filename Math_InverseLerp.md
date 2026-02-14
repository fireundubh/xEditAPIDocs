# InverseLerp

## Syntax

```pascal
function InverseLerp(A, B, AValue: Double): Double;
```

## Description

Calculates the linear interpolation factor that would result in `AValue` when interpolating between `A` and `B`.

The result is clamped between 0 and 1.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| A | Double | The start value of the range |
| B | Double | The end value of the range |
| AValue | Double | The value to find the interpolation factor for |

## Returns

Returns the interpolation factor (0 to 1) that produces AValue when interpolating between A and B.

## Example

```pascal
f := InverseLerp(10, 20, 15);
AddMessage(FloatToStr(f)); // Output: 0.5
```

## See Also

- [Lerp](Math_Lerp.md)
- [LerpUnclamped](Math_LerpUnclamped.md)
