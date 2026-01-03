# DefType

## Syntax

```pascal
function DefType(AElement: IwbElement): TwbDefType;
```

## Description

Returns the definition type of the element.

This function returns the def-type of the element, which describes the fundamental type of the element's definition in the record structure.

## Example

```pascal
var
  element: IwbElement;
  defType: TwbDefType;
begin
  defType := DefType(element);
  // Use the definition type information
end;
```

## See Also

- [ElementType](IwbElement_ElementType.md)
