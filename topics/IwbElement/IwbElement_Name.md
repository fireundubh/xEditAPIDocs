# Name

## Syntax

```pascal
function Name(AElement: IwbElement): string;
```

## Description

Returns the basic name of the element.

This function returns the standard name of the element. This is the most commonly used name function and returns a basic identifier for the element.

## Example

```pascal
var
    element: IwbElement;
    elementName: string;
begin
    elementName := Name(element);
    // Use the element name
end;
```

## See Also

- [BaseName](IwbElement_BaseName.md)
- [ShortName](IwbElement_ShortName.md)
- [DisplayName](IwbElement_DisplayName.md)
