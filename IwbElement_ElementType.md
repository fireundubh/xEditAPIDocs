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
// Example 1: Type-based element processing
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  elemType: TwbElementType;
  elemName: string;
begin
  if Assigned(e) then begin
    container := e;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        elemType := ElementType(element);
        elemName := Name(element);
        case elemType of
          etSubRecord: AddMessage(Format('Subrecord: %s', [elemName]));
          etArray: AddMessage(Format('Array: %s (%d elements)',
            [elemName, ElementCount(element)]));
          etStruct: AddMessage(Format('Struct: %s', [elemName]));
          etValue: AddMessage(Format('Value: %s = %s',
            [elemName, GetEditValue(element)]));
        end;
      end;
    end;
  end;
end;

// Example 2: Filter by element type
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  arrayCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    arrayCount := 0;
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) and (ElementType(element) = etArray) then begin
        Inc(arrayCount);
        AddMessage(Format('Array found: %s', [Name(element)]));
      end;
    end;
    AddMessage(Format('Total arrays in record: %d', [arrayCount]));
  end;
end;

// Example 3: Type-safe container casting
var
  rec: IwbMainRecord;
  element: IwbElement;
  elemType: TwbElementType;
  container: IwbContainer;
  i: integer;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'KWDA');
    if Assigned(element) then begin
      elemType := ElementType(element);
      if elemType in [etArray, etStruct, etSubRecord, etSubRecordStruct, etSubRecordArray] then begin
        container := element;
        AddMessage(Format('Container type %s has %d children',
          [ElementTypeAsText(element), ElementCount(container)]));
      end else
        AddMessage('Element is not a container type');
    end;
  end;
end;
```

## See Also

- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)
- [DefType](IwbElement_DefType.md)
- [DefTypeAsText](IwbElement_DefTypeAsText.md)
- [Check](IwbElement_Check.md)


