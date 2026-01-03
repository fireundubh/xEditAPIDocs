# InRange

## Syntax

```pascal
function InRange(AValue, AMin, AMax: Integer): Boolean;
function InRange(AValue, AMin, AMax: Single): Boolean;
function InRange(AValue, AMin, AMax: Double): Boolean;
```

## Description

Returns `True` if `AValue` is within the range specified by `AMin` and `AMax` (inclusive).

## Example

```pascal
if InRange(5, 1, 10) then
  AddMessage('5 is between 1 and 10');
```
