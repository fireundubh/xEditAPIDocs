# GetElementEditValues

## Syntax

```pascal
function GetElementEditValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the edit value of an element in the container by path as a string. This is the value as it would appear in the editor.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the value from |
| APath | string | The element path to the value |

## Returns

Returns the edit value as a string.

## Example

```pascal
// Example 1: Read nested struct value
var
  rec: IwbMainRecord;
  value, weight: string;
begin
  if Assigned(e) then begin
    value := GetElementEditValues(e, 'DATA\Value');
    weight := GetElementEditValues(e, 'DATA\Weight');
    AddMessage(Format('Value: %s, Weight: %s', [value, weight]));
  end;
end;

// Example 2: Read array element value
var
  rec: IwbMainRecord;
  firstKeyword: string;
begin
  if Assigned(e) then begin
    firstKeyword := GetElementEditValues(e, 'KWDA\[0]');
    if firstKeyword <> '' then
      AddMessage('First keyword: ' + firstKeyword)
    else
      AddMessage('No keywords or empty value');
  end;
end;

// Example 3: Batch read multiple field values
var
  rec: IwbMainRecord;
  editorID, fullName, modelPath: string;
  value, weight, health: string;
begin
  if Assigned(e) then begin
    // Read basic fields
    editorID := GetElementEditValues(e, 'EDID');
    fullName := GetElementEditValues(e, 'FULL');
    modelPath := GetElementEditValues(e, 'Model\MODL');

    // Read DATA struct fields
    value := GetElementEditValues(e, 'DATA\Value');
    weight := GetElementEditValues(e, 'DATA\Weight');
    health := GetElementEditValues(e, 'DATA\Health');

    AddMessage('Record Details:');
    AddMessage(Format('  EDID: %s', [editorID]));
    AddMessage(Format('  FULL: %s', [fullName]));
    AddMessage(Format('  Model: %s', [modelPath]));
    AddMessage(Format('  Value: %s, Weight: %s, Health: %s',
      [value, weight, health]));
  end;
end;

// Example 4: Read condition function value
var
  rec: IwbMainRecord;
  functionName, comparisonValue: string;
begin
  if Assigned(e) then begin
    functionName := GetElementEditValues(e, 'Conditions\[0]\CTDA\Function');
    comparisonValue := GetElementEditValues(e, 'Conditions\[0]\CTDA\Comparison Value');

    if functionName <> '' then
      AddMessage(Format('First condition: %s = %s', [functionName, comparisonValue]))
    else
      AddMessage('No conditions found');
  end;
end;
```

## See Also

- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)
- [GetElementValues](IwbContainer_GetElementValues.md)
- [GetEditValue](IwbElement_GetEditValue.md)


