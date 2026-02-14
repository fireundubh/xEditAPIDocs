# InRange

## Syntax

```pascal
function InRange(AValue, AMin, AMax: Integer): Boolean;
function InRange(AValue, AMin, AMax: Single): Boolean;
function InRange(AValue, AMin, AMax: Double): Boolean;
```

## Description

Returns `True` if `AValue` is within the range specified by `AMin` and `AMax` (inclusive).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | Integer/Single/Double | The value to check |
| AMin | Integer/Single/Double | The minimum value of the range (inclusive) |
| AMax | Integer/Single/Double | The maximum value of the range (inclusive) |

## Returns

Returns `True` if AValue is within the range [AMin, AMax], `False` otherwise.

## Example

```pascal
if InRange(5, 1, 10) then
  AddMessage('5 is between 1 and 10');
```
