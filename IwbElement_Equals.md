# Equals

## Syntax

```pascal
function Equals(ASource: IwbElement; ATarget: IwbElement): boolean;
```

## Description

Compares two elements by their ElementID.

This function is sometimes necessary because different IInterface variables pointing to the same element don't always compare properly when using the = operator.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ASource | IwbElement | The first element to compare |
| ATarget | IwbElement | The second element to compare |

## Returns

Returns true if both elements have the same ElementID, false otherwise.

## Example

```pascal
var
  element1, element2: IwbElement;
  areEqual: boolean;
begin
  areEqual := Equals(element1, element2);
  if areEqual then
    // Elements are the same
end;
```

## See Also

- [SortKey](IwbElement_SortKey.md)


