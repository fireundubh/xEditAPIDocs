# ShortName

## Syntax

```pascal
function ShortName(AElement: IwbElement): string;
```

## Description

Returns a compact name representation optimized for display in limited space.

This function retrieves the ShortName property, which provides an abbreviated element identifier. The exact abbreviation strategy varies by element type but typically omits verbose prefixes or truncates long names. Useful for UI elements like tree views where space is limited. Returns an empty string for invalid elements. Generally shorter than Name but may be identical for simple elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose short name to retrieve |

## Returns

Returns a shortened version of the element's name as a string.

## Example

```pascal
var
    element: IwbElement;
    shortName: string;
begin
    shortName := ShortName(element);
    // Use the shortened name
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [DisplayName](IwbElement_DisplayName.md)
- [PathName](IwbElement_PathName.md)


