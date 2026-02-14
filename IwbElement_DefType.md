# DefType

## Syntax

```pascal
function DefType(AElement: IwbElement): TwbDefType;
```

## Description

Returns the definition type enumeration value for the element's value definition.

This function retrieves the element's ValueDef and returns its DefType property, which categorizes the data type (e.g., dtInteger, dtFloat, dtString, dtFormID, dtStruct, dtArray). Returns -1 if the element is invalid or has no ValueDef. The DefType determines how the element's data is interpreted and stored. More granular than ElementType, which describes the element's structural role.

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

- [DefTypeAsText](IwbElement_DefTypeAsText.md)
- [ElementType](IwbElement_ElementType.md)
- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)


