# ElementType

## Syntax

```pascal
function ElementType(AElement: IwbElement): TwbElementType;
```

## Description

Returns the structural element type enumeration value.

This function retrieves the ElementType property, which categorizes the element's role in the record hierarchy (e.g., etFile, etMainRecord, etGroupRecord, etSubRecord, etArray, etStruct, etValue). Returns -1 for invalid elements. The ElementType determines what interfaces the element supports and how it should be processed. Different from DefType, which describes the data type rather than structural role.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the type for |

## Returns

Returns a TwbElementType enumeration value representing the element type.

## Element Types

- `etFile`
- `etMainRecord`
- `etGroupRecord`
- `etSubRecord`
- `etSubRecordStruct`
- `etSubRecordArray`
- `etSubRecordUnion`
- `etArray`
- `etStruct`
- `etValue`
- `etFlag`
- `etStringListTerminator`
- `etUnion`
- `etStructChapter`

## Example

```pascal
var
  element: IwbElement;
  elemType: TwbElementType;
begin
  elemType := ElementType(element);
  case elemType of
    etFile: // Handle file element
    etMainRecord: // Handle main record
    etSubRecord: // Handle subrecord
  end;
end;
```

## See Also

- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)
- [DefType](IwbElement_DefType.md)
- [DefTypeAsText](IwbElement_DefTypeAsText.md)
- [Check](IwbElement_Check.md)


