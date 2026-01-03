# ElementType

## Syntax

```pascal
function ElementType(AElement: IwbElement): TwbElementType;
```

## Description

Returns the type of the element.

This function returns an enumerated value indicating the type of the element. This is useful for determining how to handle different types of elements.

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

- [Check](IwbElement_Check.md)


