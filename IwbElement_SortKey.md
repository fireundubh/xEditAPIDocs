# SortKey

## Syntax

```pascal
function SortKey(AElement: IwbElement): string;
```

## Description

Returns a string used for sorting elements.

This function returns a string that can be used to sort elements in a consistent order. The sort key may be different from the element's name and is specifically designed for proper sorting.

## Example

```pascal
var
    element: IwbElement;
    key: string;
begin
    key := SortKey(element);
    // Use the sort key for ordering
end;
```

## See Also

- [Name](IwbElement_Name.md)


