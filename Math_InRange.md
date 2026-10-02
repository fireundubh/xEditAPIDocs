# InRange

## Syntax

```pascal
function InRange(AValue, AMin, AMax: Double): Boolean;
```

## Description

Returns `True` if `AValue` is within the range specified by `AMin` and `AMax` (inclusive).

One three-argument function is registered. There are no separate integer, single, and double overloads in the script adapter.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AValue | Double | The value to check |
| AMin | Double | The minimum value of the range (inclusive) |
| AMax | Double | The maximum value of the range (inclusive) |

## Returns

Returns `True` if AValue is within the range [AMin, AMax], `False` otherwise.

## Example

```pascal
begin
  if InRange(5, 1, 10) then
    AddMessage('5 is between 1 and 10');
end;
```
