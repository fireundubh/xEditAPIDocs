# Name

## Syntax

```pascal
function Name(AElement: IwbElement): string;
```

## Description

Returns the element's standard name as defined in its element definition.

This function retrieves the Name property, which returns the element's identifier from the record structure definition. For fields, this is typically the 4-character signature (e.g., "EDID", "DATA"). For array elements, it may include an index. Returns an empty string if the element is invalid. This is the most commonly used name function for element identification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose name to retrieve |

## Returns

Returns the standard name of the element as a string.

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
- [PathName](IwbElement_PathName.md)
- [Path](IwbElement_Path.md)


