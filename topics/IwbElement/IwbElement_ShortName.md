# ShortName

## Syntax

```pascal
function ShortName(AElement: IwbElement): string;
```

## Description

Returns a shortened version of the element's name.

This function returns a concise name for the element, typically shorter than the standard `Name` function. Useful for display in space-constrained UI elements.

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

- [Name - IwbElement](IwbElement_Name.md)
- [BaseName - IwbElement](IwbElement_BaseName.md)
- [DisplayName - IwbElement](IwbElement_DisplayName.md)
- [PathName - IwbElement](IwbElement_PathName.md)
