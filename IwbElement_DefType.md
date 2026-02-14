# DefType

## Syntax

```pascal
function DefType(AElement: IwbElement): TwbDefType;
```

## Description

Returns the definition type of the element.

This function returns the def-type of the element, which describes the fundamental type of the element's definition in the record structure.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the definition type for |

## Returns

Returns a TwbDefType enumeration value representing the definition type.

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


