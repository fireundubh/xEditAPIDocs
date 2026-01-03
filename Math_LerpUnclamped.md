# LerpUnclamped

## Syntax

```pascal
function LerpUnclamped(A, B, AValue: Double): Double;
```

## Description

Linearly interpolates between `A` and `B` by the factor `AValue`.

Unlike [Lerp](Math_Lerp.md), `AValue` is not clamped.

## Example

```pascal
f := LerpUnclamped(10, 20, 1.5);
AddMessage(FloatToStr(f)); // Output: 25
```

## See Also

- [InverseLerp](Math_InverseLerp.md)
- [Lerp](Math_Lerp.md)
