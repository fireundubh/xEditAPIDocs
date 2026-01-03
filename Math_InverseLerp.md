# InverseLerp

## Syntax

```pascal
function InverseLerp(A, B, AValue: Double): Double;
```

## Description

Calculates the linear interpolation factor that would result in `AValue` when interpolating between `A` and `B`.

The result is clamped between 0 and 1.

## Example

```pascal
f := InverseLerp(10, 20, 15);
AddMessage(FloatToStr(f)); // Output: 0.5
```

## See Also

- [Lerp](Math_Lerp.md)
- [LerpUnclamped](Math_LerpUnclamped.md)
