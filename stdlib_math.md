# Mathematics Reference

Advanced mathematical functions including trigonometry, logarithms, hyperbolic functions, and financial calculations.

**Unit:** Math

[← Back to Standard Library Overview](stdlib_home.md)

## Table of Contents

- [Power and Roots](#power-and-roots)
- [Logarithms](#logarithms)
- [Trigonometric Functions](#trigonometric-functions)
- [Inverse Trigonometric](#inverse-trigonometric)
- [Hyperbolic Functions](#hyperbolic-functions)
- [Angle Conversion](#angle-conversion)
- [Rounding and Comparison](#rounding-and-comparison)
- [Special Functions](#special-functions)
- [Random Functions](#random-functions)
- [Financial Functions](#financial-functions)
- [Constants](#constants)

## Power and Roots

| Function | Signature | Description |
|----------|-----------|-------------|
| **`Power`** | `Power(Base, Exponent: Extended): Extended` | Base^Exponent (floating-point exponent) |
| **`IntPower`** | `IntPower(Base: Extended, Exponent: Integer): Extended` | Base^Exponent (integer exponent, faster) |
| `Ldexp` | `Ldexp(X: Extended, P: Integer): Extended` | X × 2^P (fast multiply by power of 2) |
| `Frexp` | `Frexp(X: Extended, var Exponent: Integer): Extended` | Split X into mantissa and exponent |

### Examples

```pascal
var
  result: Extended;
begin
  // Floating-point exponents
  result := Power(2, 10);      // 1024.0
  result := Power(2, 0.5);     // 1.414... (square root of 2)
  result := Power(10, -3);     // 0.001

  // Integer exponents (faster)
  result := IntPower(2, 10);   // 1024.0
  result := IntPower(3, 4);    // 81.0
  result := IntPower(5, -2);   // 0.04

  // Fast power-of-2 operations
  result := Ldexp(1.5, 4);     // 1.5 × 2^4 = 24.0
  result := Ldexp(3.0, -2);    // 3.0 × 2^-2 = 0.75
end;
```

### xEdit Example: Calculate Level Scaling
```pascal
// Calculate scaled value using power function
function ScaleValueByLevel(baseValue: Extended; level, maxLevel: Integer): Extended;
var
  scaleFactor: Extended;
begin
  // Non-linear scaling: value increases faster at higher levels
  scaleFactor := Power(level / maxLevel, 1.5);
  Result := baseValue * (1 + scaleFactor * 2);
end;

var
  baseHealth: Extended;
  level, npcLevel: Integer;
begin
  baseHealth := 100.0;
  npcLevel := 50;

  AddMessage(Format('Level %d health: %.0f', [
    npcLevel,
    ScaleValueByLevel(baseHealth, npcLevel, 100)
  ]));
end;
```

## Logarithms

| Function | Signature | Description |
|----------|-----------|-------------|
| `Ln` | `Ln(X: Extended): Extended` | Natural logarithm (base e) |
| **`Log10`** | `Log10(X: Extended): Extended` | Base-10 logarithm |
| **`Log2`** | `Log2(X: Extended): Extended` | Base-2 logarithm |
| **`LogN`** | `LogN(Base, X: Extended): Extended` | Base-N logarithm |
| `LnXP1` | `LnXP1(X: Extended): Extended` | Ln(X + 1) - more accurate for small X |
| `Exp` | `Exp(X: Extended): Extended` | e^X (exponential) |

### Examples

```pascal
var
  result: Extended;
begin
  result := Log10(1000);        // 3.0
  result := Log10(100);         // 2.0
  result := Log2(256);          // 8.0
  result := Log2(1024);         // 10.0
  result := LogN(5, 125);       // 3.0 (5^3 = 125)

  // Inverse of Log is Power
  result := Power(10, 3);       // 1000.0 (inverse of Log10(1000))
  result := Power(2, 8);        // 256.0 (inverse of Log2(256))
end;
```

### xEdit Example: Logarithmic Distribution
```pascal
// Distribute items using logarithmic scale
function CalculateDropChance(itemValue: Extended): Extended;
var
  normalizedValue: Extended;
begin
  // Higher value items have exponentially lower drop chance
  // Values: 1-1000 gold
  normalizedValue := Log10(itemValue) / Log10(1000);  // 0.0 to 1.0
  Result := 1.0 - normalizedValue;  // Invert so cheap items = high chance
end;

var
  value: Extended;
begin
  value := 1;
  AddMessage(Format('%d gold: %.1f%% drop chance', [
    Round(value),
    CalculateDropChance(value) * 100
  ]));  // 100% chance

  value := 100;
  AddMessage(Format('%d gold: %.1f%% drop chance', [
    Round(value),
    CalculateDropChance(value) * 100
  ]));  // ~33% chance

  value := 1000;
  AddMessage(Format('%d gold: %.1f%% drop chance', [
    Round(value),
    CalculateDropChance(value) * 100
  ]));  // 0% chance
end;
```

## Trigonometric Functions

**Note:** All trig functions use **radians**, not degrees. Use [angle conversion](#angle-conversion) functions to convert.

| Function | Signature | Description |
|----------|-----------|-------------|
| `Sin` | `Sin(X: Extended): Extended` | Sine |
| `Cos` | `Cos(X: Extended): Extended` | Cosine |
| `Tan` | `Tan(X: Extended): Extended` | Tangent |
| **`Cot`** | `Cot(X: Extended): Extended` | Cotangent (1 / tan) |
| **`Sec`** | `Sec(X: Extended): Extended` | Secant (1 / cos) |
| **`Csc`** | `Csc(X: Extended): Extended` | Cosecant (1 / sin) |

### Examples

```pascal
var
  angle, result: Extended;
begin
  angle := DegToRad(45);  // Convert 45° to radians

  result := Sin(angle);    // 0.707...
  result := Cos(angle);    // 0.707...
  result := Tan(angle);    // 1.0

  // Pythagorean identity: sin² + cos² = 1
  result := Sqr(Sin(angle)) + Sqr(Cos(angle));  // 1.0
end;
```

### xEdit Example: Calculate Projectile Trajectory
```pascal
// Calculate projectile landing distance
function ProjectileDistance(velocity, angleRad, gravity: Extended): Extended;
var
  vx, vy, timeOfFlight: Extended;
begin
  vx := velocity * Cos(angleRad);  // Horizontal component
  vy := velocity * Sin(angleRad);  // Vertical component

  timeOfFlight := (2 * vy) / gravity;
  Result := vx * timeOfFlight;
end;

var
  angle, velocity, distance: Extended;
begin
  velocity := 100.0;  // units per second
  angle := DegToRad(30);  // 30 degree angle

  distance := ProjectileDistance(velocity, angle, 9.8);
  AddMessage(Format('Projectile lands %.2f units away', [distance]));
end;
```

## Inverse Trigonometric

| Function | Signature | Description |
|----------|-----------|-------------|
| `ArcTan` | `ArcTan(X: Extended): Extended` | Arctangent (result in radians) |
| **`ArcTan2`** | `ArcTan2(Y, X: Extended): Extended` | Arctangent of Y/X (handles all quadrants) |
| **`ArcSin`** | `ArcSin(X: Extended): Extended` | Arcsine (X must be in [-1, 1]) |
| **`ArcCos`** | `ArcCos(X: Extended): Extended` | Arccosine (X must be in [-1, 1]) |

### Examples

```pascal
var
  x, y, angle: Extended;
begin
  // ArcTan2 handles all quadrants correctly
  x := 1.0;
  y := 1.0;
  angle := ArcTan2(y, x);  // 45° (0.785 radians)
  AddMessage(Format('Angle: %.0f degrees', [RadToDeg(angle)]));

  x := -1.0;
  y := 1.0;
  angle := ArcTan2(y, x);  // 135° (2.356 radians)
  AddMessage(Format('Angle: %.0f degrees', [RadToDeg(angle)]));

  // ArcSin / ArcCos
  angle := ArcSin(0.5);  // 30° (0.524 radians)
  angle := ArcCos(0.5);  // 60° (1.047 radians)
end;
```

### xEdit Example: Calculate Angle Between Points
```pascal
// Calculate direction angle between two 2D points
function AngleBetweenPoints(x1, y1, x2, y2: Extended): Extended;
var
  dx, dy: Extended;
begin
  dx := x2 - x1;
  dy := y2 - y1;
  Result := ArcTan2(dy, dx);  // Returns angle in radians
end;

var
  angle: Extended;
begin
  angle := AngleBetweenPoints(0, 0, 10, 10);
  AddMessage(Format('Angle: %.0f degrees', [RadToDeg(angle)]));  // 45°

  angle := AngleBetweenPoints(10, 10, 0, 0);
  AddMessage(Format('Angle: %.0f degrees', [RadToDeg(angle)]));  // -135°
end;
```

## Hyperbolic Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| **`Sinh`** | `Sinh(X: Extended): Extended` | Hyperbolic sine |
| **`Cosh`** | `Cosh(X: Extended): Extended` | Hyperbolic cosine |
| **`Tanh`** | `Tanh(X: Extended): Extended` | Hyperbolic tangent |
| **`CotH`** | `CotH(X: Extended): Extended` | Hyperbolic cotangent |
| **`SecH`** | `SecH(X: Extended): Extended` | Hyperbolic secant |
| **`CscH`** | `CscH(X: Extended): Extended` | Hyperbolic cosecant |
| **`ArcSinh`** | `ArcSinh(X: Extended): Extended` | Inverse hyperbolic sine |
| **`ArcCosh`** | `ArcCosh(X: Extended): Extended` | Inverse hyperbolic cosine |
| **`ArcTanh`** | `ArcTanh(X: Extended): Extended` | Inverse hyperbolic tangent |

### Example

```pascal
var
  x, result: Extended;
begin
  x := 1.0;
  result := Sinh(x);     // 1.175...
  result := Cosh(x);     // 1.543...
  result := Tanh(x);     // 0.762...

  // Identity: cosh² - sinh² = 1
  result := Sqr(Cosh(x)) - Sqr(Sinh(x));  // 1.0
end;
```

## Angle Conversion

Convert between degrees, radians, grads (gradians), and cycles.

### Common Conversions

| Function | Description | Example |
|----------|-------------|---------|
| **`DegToRad`** | Degrees to radians | `DegToRad(180)` → `3.14159` (π) |
| **`RadToDeg`** | Radians to degrees | `RadToDeg(3.14159)` → `180` |
| `DegToGrad` | Degrees to grads | `DegToGrad(90)` → `100` |
| `GradToDeg` | Grads to degrees | `GradToDeg(100)` → `90` |

### All Conversion Functions

12 functions cover all combinations:
- **Degrees** ↔ Radians, Grads, Cycles
- **Radians** ↔ Degrees, Grads, Cycles
- **Grads** ↔ Degrees, Radians, Cycles
- **Cycles** ↔ Degrees, Radians, Grads

**Unit circle:**
- 360 degrees = 2π radians = 400 grads = 1 cycle

```pascal
var
  angle: Extended;
begin
  // Degrees to radians (most common)
  angle := DegToRad(90);      // π/2 = 1.5708

  // Radians to degrees
  angle := RadToDeg(3.14159); // 180

  // Grads (used in surveying)
  angle := DegToGrad(90);     // 100 grads
  angle := GradToDeg(100);    // 90 degrees

  // Cycles (full rotations)
  angle := DegToCycle(360);   // 1.0 cycle
  angle := CycleToDeg(0.5);   // 180 degrees
end;
```

### xEdit Example: Normalize Rotation Angles
```pascal
// Normalize rotation angle to 0-360 degrees
function NormalizeAngle(degrees: Extended): Extended;
begin
  Result := degrees;
  while Result >= 360 do
    Result := Result - 360;
  while Result < 0 do
    Result := Result + 360;
end;

// Convert rotation from radians to normalized degrees
function RadToNormalizedDeg(radians: Extended): Extended;
begin
  Result := NormalizeAngle(RadToDeg(radians));
end;
```

## Rounding and Comparison

| Function | Signature | Description |
|----------|-----------|-------------|
| `Round` | `Round(X: Extended): Integer` | Round to nearest integer (banker's rounding) |
| `Trunc` | `Trunc(X: Extended): Integer` | Truncate (remove decimals) |
| **`Floor`** | `Floor(X: Extended): Integer` | Round down (largest integer ≤ X) |
| **`Ceil`** | `Ceil(X: Extended): Integer` | Round up (smallest integer ≥ X) |
| **`Max`** | `Max(A, B: Integer): Integer` | Maximum of two values |
| **`Min`** | `Min(A, B: Integer): Integer` | Minimum of two values |
| `MaxValue` | `MaxValue(const Data: array of Extended): Extended` | Maximum in array |
| `MinValue` | `MinValue(const Data: array of Extended): Extended` | Minimum in array |
| `MaxIntValue` | `MaxIntValue(const Data: array of Integer): Integer` | Maximum integer in array |
| `MinIntValue` | `MinIntValue(const Data: array of Integer): Integer` | Minimum integer in array |
| **`InRange`** | `InRange(Value, Min, Max: Integer): Boolean` | Check if value in range [Min, Max] |
| **`EnsureRange`** | `EnsureRange(Value, Min, Max: Integer): Integer` | Clamp value to range |
| `CompareValue` | `CompareValue(A, B: Extended, Epsilon: Extended = 0): Integer` | Compare floats (returns -1, 0, 1) |
| `SameValue` | `SameValue(A, B: Extended, Epsilon: Extended = 0): Boolean` | Test if floats are equal |

### Examples

```pascal
var
  x: Extended;
  i, result: Integer;
begin
  // Rounding
  x := 3.7;
  result := Round(x);  // 4
  result := Trunc(x);  // 3
  result := Floor(x);  // 3
  result := Ceil(x);   // 4

  x := -3.7;
  result := Round(x);  // -4
  result := Trunc(x);  // -3
  result := Floor(x);  // -4 (rounds down = more negative)
  result := Ceil(x);   // -3 (rounds up = less negative)

  // Min/Max
  result := Max(10, 20);     // 20
  result := Min(10, 20);     // 10

  // Range checking
  if InRange(15, 10, 20) then
    AddMessage('15 is in range [10, 20]');

  // Clamp to range
  result := EnsureRange(25, 10, 20);  // 20 (clamped)
  result := EnsureRange(5, 10, 20);   // 10 (clamped)
  result := EnsureRange(15, 10, 20);  // 15 (unchanged)
end;
```

### xEdit Example: Clamp and Validate Values
```pascal
// Validate and clamp element values
procedure ValidateArmorRating(element: IwbElement);
var
  value, clamped: Integer;
begin
  value := StrToIntDef(GetEditValue(element), 0);

  // Clamp to valid range
  clamped := EnsureRange(value, 0, 100);

  if value <> clamped then begin
    AddMessage(Format('Clamped armor rating from %d to %d', [value, clamped]));
    SetEditValue(element, IntToStr(clamped));
  end;
end;

// Find highest value record
function FindMaxValue(const values: array of Extended): Extended;
begin
  Result := MaxValue(values);
end;
```

## Special Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| **`Hypot`** | `Hypot(X, Y: Extended): Extended` | Hypotenuse: √(X² + Y²) |
| `IsNan` | `IsNan(const Value: Extended): Boolean` | Check if Not-a-Number |
| `IsInfinite` | `IsInfinite(const Value: Extended): Boolean` | Check if ±infinity |
| `IsZero` | `IsZero(const Value: Extended, Epsilon: Extended = 0): Boolean` | Check if zero (with tolerance) |
| `Sign` | `Sign(const Value: Integer): TValueSign` | Get sign: -1, 0, or 1 |

### Examples

```pascal
var
  x, y, distance: Extended;
  result: Boolean;
begin
  // Calculate distance (hypotenuse)
  x := 3.0;
  y := 4.0;
  distance := Hypot(x, y);  // 5.0 (√(9 + 16))

  // More accurate than Sqrt(Sqr(x) + Sqr(y)) for very large/small values

  // Check for invalid values
  x := 0.0 / 0.0;  // NaN
  if IsNan(x) then
    AddMessage('Value is Not-a-Number');

  x := 1.0 / 0.0;  // Infinity
  if IsInfinite(x) then
    AddMessage('Value is infinite');

  // Check if effectively zero
  x := 0.00000001;
  if IsZero(x, 0.0001) then
    AddMessage('Value is effectively zero');
end;
```

### xEdit Example: Calculate 3D Distance
```pascal
// Calculate distance between two 3D points
function Distance3D(x1, y1, z1, x2, y2, z2: Extended): Extended;
var
  dx, dy, dz: Extended;
begin
  dx := x2 - x1;
  dy := y2 - y1;
  dz := z2 - z1;

  // Method 1: Using Hypot twice (more accurate)
  Result := Hypot(Hypot(dx, dy), dz);

  // Method 2: Direct calculation
  // Result := Sqrt(Sqr(dx) + Sqr(dy) + Sqr(dz));
end;
```

## Random Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| `Randomize` | `Randomize()` | Initialize random generator (call once) |
| `Random` | `Random(): Extended` | Random float in [0.0, 1.0) |
| `Random` | `Random(Range: Integer): Integer` | Random integer in [0, Range-1] |
| **`RandomRange`** | `RandomRange(AFrom, ATo: Integer): Integer` | Random integer in [AFrom, ATo-1] |
| **`RandG`** | `RandG(Mean, StdDev: Extended): Extended` | Gaussian (normal) random number |

### Examples

```pascal
var
  i, randomInt: Integer;
  randomFloat: Extended;
begin
  Randomize();  // Initialize (call once at start)

  // Random float [0.0, 1.0)
  randomFloat := Random();
  AddMessage(Format('Random float: %.3f', [randomFloat]));

  // Random integer [0, 99]
  randomInt := Random(100);
  AddMessage(Format('Random 0-99: %d', [randomInt]));

  // Random integer in specific range [10, 20]
  randomInt := RandomRange(10, 21);  // Note: upper bound is exclusive
  AddMessage(Format('Random 10-20: %d', [randomInt]));

  // Gaussian distribution (bell curve)
  randomFloat := RandG(100, 15);  // Mean=100, StdDev=15
  AddMessage(Format('Gaussian random: %.2f', [randomFloat]));
end;
```

### xEdit Example: Random Record Selection and Variation
```pascal
// Select random records from a file
procedure SelectRandomRecords(f: IwbFile; count: Integer);
var
  i, randomIndex, totalRecords: Integer;
  rec: IwbMainRecord;
  selected: TStringList;
  formIDStr: string;
begin
  Randomize();
  totalRecords := RecordCount(f);

  selected := TStringList.Create;
  try
    selected.Sorted := True;  // Enable fast duplicate checking

    for i := 1 to count do begin
      randomIndex := Random(totalRecords);
      rec := RecordByIndex(f, randomIndex);
      formIDStr := IntToHex(rec.FormID, 8);

      // Check if already selected
      if selected.IndexOf(formIDStr) = -1 then begin
        selected.Add(formIDStr);
        AddMessage(Format('Selected: %s [%s]', [rec.EditorID, formIDStr]));
      end;
    end;
  finally
    selected.Free;
  end;
end;

// Add random variation to values (Gaussian distribution)
function AddVariation(baseValue, variationPercent: Extended): Extended;
var
  stdDev, variation: Extended;
begin
  stdDev := baseValue * (variationPercent / 100) / 2;  // ~95% within range
  variation := RandG(0, stdDev);  // Mean=0, random offset
  Result := baseValue + variation;
end;
```

## Financial Functions

| Function | Signature | Description |
|----------|-----------|-------------|
| **`SLNDepreciation`** | `SLNDepreciation(Cost, Salvage, Life: Extended): Extended` | Straight-line depreciation |
| **`SYDDepreciation`** | `SYDDepreciation(Cost, Salvage, Life, Period: Extended): Extended` | Sum-of-years-digits depreciation |
| `FutureValue` | `FutureValue(Rate: Extended, NPeriods: Integer, Payment, PresentValue: Extended, PaymentTime: TPaymentTime): Extended` | Future value of investment |
| `PresentValue` | `PresentValue(Rate: Extended, NPeriods: Integer, Payment, FutureValue: Extended, PaymentTime: TPaymentTime): Extended` | Present value |
| `InterestPayment` | `InterestPayment(Rate: Extended, Period, NPeriods: Integer, PresentValue, FutureValue: Extended, PaymentTime: TPaymentTime): Extended` | Interest payment for period |

### Example: Depreciation

```pascal
var
  cost, salvage, life: Extended;
  depreciationPerYear: Extended;
begin
  cost := 10000;    // Initial cost
  salvage := 1000;  // Salvage value at end
  life := 5;        // Years of useful life

  // Straight-line: same depreciation each year
  depreciationPerYear := SLNDepreciation(cost, salvage, life);
  AddMessage(Format('SLN Depreciation per year: %.2f', [depreciationPerYear]));
  // Result: 1800 per year

  // Sum-of-years-digits: higher depreciation in early years
  for i := 1 to 5 do begin
    depreciationPerYear := SYDDepreciation(cost, salvage, life, i);
    AddMessage(Format('Year %d SYD Depreciation: %.2f', [i, depreciationPerYear]));
  end;
end;
```

## Constants

Mathematical constants available in the Math unit:

```pascal
Pi = 3.14159265358979323846;
```

Use `DegToRad` and `RadToDeg` instead of multiplying by Pi/180 directly.

---

[← Back to Standard Library Overview](stdlib_home.md) | [Next: User Interface →](stdlib_ui.md)
