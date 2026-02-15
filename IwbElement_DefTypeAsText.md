# DefTypeAsText

## Syntax

```pascal
function DefTypeAsText(AElement: IwbElement): String;
```

## Description

Returns the definition type of `AElement` as a string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the definition type from |

## Returns

Returns the definition type as a string.

## Example

```pascal
// Example 1: Display element definition type
var
  element: IwbElement;
  defTypeText: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'DATA\Value');
    if Assigned(element) then begin
      defTypeText := DefTypeAsText(element);
      AddMessage(Format('%s definition type: %s',
        [Name(element), defTypeText]));
    end;
  end;
end;

// Example 2: Categorize elements by data type
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  defType: string;
  numericCount, stringCount, otherCount: integer;
begin
  if Assigned(e) then begin
    container := e;
    numericCount := 0;
    stringCount := 0;
    otherCount := 0;

    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        defType := DefTypeAsText(element);
        if Pos('Integer', defType) > 0 then
          Inc(numericCount)
        else if Pos('Float', defType) > 0 then
          Inc(numericCount)
        else if Pos('String', defType) > 0 then
          Inc(stringCount)
        else
          Inc(otherCount);
      end;
    end;

    AddMessage(Format('%s data types:', [EditorID(e)]));
    AddMessage(Format('  Numeric: %d', [numericCount]));
    AddMessage(Format('  String: %d', [stringCount]));
    AddMessage(Format('  Other: %d', [otherCount]));
  end;
end;

// Example 3: Validate expected definition types
var
  weightElement, valueElement: IwbElement;
  weightType, valueType: string;
begin
  if Assigned(e) then begin
    weightElement := ElementByPath(e, 'DATA\Weight');
    valueElement := ElementByPath(e, 'DATA\Value');

    if Assigned(weightElement) then begin
      weightType := DefTypeAsText(weightElement);
      if weightType = 'dtFloat' then
        AddMessage('Weight type correct: ' + weightType)
      else
        AddMessage('WARNING: Unexpected weight type: ' + weightType);
    end;

    if Assigned(valueElement) then begin
      valueType := DefTypeAsText(valueElement);
      if valueType = 'dtInteger' then
        AddMessage('Value type correct: ' + valueType)
      else
        AddMessage('WARNING: Unexpected value type: ' + valueType);
    end;
  end;
end;
```

## See Also

- [DefType](IwbElement_DefType.md)
- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)
