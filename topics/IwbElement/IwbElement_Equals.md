# Equals

## Syntax

```pascal
function Equals(ASource: IwbElement; ATarget: IwbElement): boolean;
```

## Description

Compares two elements by their ElementID.

This function is sometimes necessary because different IInterface variables pointing to the same element don't always compare properly when using the = operator.

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
