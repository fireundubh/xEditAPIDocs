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
// Example 1: Type-aware value extraction
var
  rec: IwbMainRecord;
  element: IwbElement;
  defType: TwbDefType;
  intValue: integer;
  floatValue: single;
  stringValue: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(rec, 'DATA\Value');
    if Assigned(element) then begin
      defType := DefType(element);
      case defType of
        dtInteger, dtInt64:
          begin
            intValue := GetNativeValue(element);
            AddMessage(Format('Integer value: %d', [intValue]));
          end;
        dtFloat:
          begin
            floatValue := GetNativeValue(element);
            AddMessage(Format('Float value: %.2f', [floatValue]));
          end;
        dtString, dtLString, dtLenString:
          begin
            stringValue := GetEditValue(element);
            AddMessage(Format('String value: %s', [stringValue]));
          end;
      end;
    end;
  end;
end;

// Example 2: Validate expected data types
var
  rec: IwbMainRecord;
  weightElement: IwbElement;
  defType: TwbDefType;
begin
  if Assigned(e) then begin
    weightElement := ElementByPath(rec, 'DATA\Weight');
    if Assigned(weightElement) then begin
      defType := DefType(weightElement);
      if defType = dtFloat then
        AddMessage(Format('Weight is correctly typed as float: %.2f',
          [GetNativeValue(weightElement)]))
      else
        AddMessage(Format('ERROR: Weight has unexpected type: %s',
          [DefTypeAsText(weightElement)]));
    end;
  end;
end;

// Example 3: Build type statistics
var
  rec: IwbMainRecord;
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  defType: TwbDefType;
  intCount, floatCount, stringCount, otherCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    intCount := 0;
    floatCount := 0;
    stringCount := 0;
    otherCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        defType := DefType(element);
        case defType of
          dtInteger, dtInt64: Inc(intCount);
          dtFloat: Inc(floatCount);
          dtString, dtLString, dtLenString: Inc(stringCount);
          else Inc(otherCount);
        end;
      end;
    end;

    AddMessage(Format('Type statistics for %s:', [EditorID(rec)]));
    AddMessage(Format('  Integers: %d', [intCount]));
    AddMessage(Format('  Floats: %d', [floatCount]));
    AddMessage(Format('  Strings: %d', [stringCount]));
    AddMessage(Format('  Other: %d', [otherCount]));
  end;
end;
```

## See Also

- [DefTypeAsText](IwbElement_DefTypeAsText.md)
- [ElementType](IwbElement_ElementType.md)
- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)


