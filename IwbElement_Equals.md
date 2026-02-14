# Equals

## Syntax

```pascal
function Equals(ASource: IwbElement; ATarget: IwbElement): boolean;
```

## Description

Compares two element references to determine if they point to the same element instance.

This function calls the first element's Equals method with the second element as the argument. Returns true if both references point to the exact same element object in memory. This is necessary because interface comparison with = can fail when different interface types wrap the same object. Use this for reliable element identity checking. Returns false for invalid elements or mismatched elements.

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


