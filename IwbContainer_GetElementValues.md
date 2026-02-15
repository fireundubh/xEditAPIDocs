# GetElementValues

## Syntax

```pascal
function GetElementValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the string display value of an element in the container by path. Useful for things like decoded texture hashes and such.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the value from |
| APath | string | The element path to the value |

## Returns

Returns the display value as a string.

## Example

```pascal
// Example 1: Get decoded texture hash
var
  textureHash: string;
begin
  if Assigned(e) then begin
    textureHash := GetElementValues(e, 'Model\MODT\Textures\Texture\File Hash');
    if textureHash <> '' then
      AddMessage('Texture hash (decoded): ' + textureHash)
    else
      AddMessage('No texture hash found');
  end;
end;

// Example 2: Get display value for complex fields
var
  formVersion, flags: string;
begin
  if Assigned(e) then begin
    // GetElementValues returns decoded/formatted display strings
    formVersion := GetElementValues(e, 'Record Header\Form Version');
    flags := GetElementValues(e, 'Record Header\Record Flags');

    AddMessage('Form Version: ' + formVersion);
    AddMessage('Flags: ' + flags);
  end;
end;

// Example 3: Read formatted data vs edit value
var
  editValue, displayValue: string;
begin
  if Assigned(e) then begin
    // Edit value might be raw hex
    editValue := GetElementEditValues(e, 'Model\MODT');

    // Display value is decoded/formatted for UI
    displayValue := GetElementValues(e, 'Model\MODT');

    AddMessage('Edit value: ' + editValue);
    AddMessage('Display value: ' + displayValue);
  end;
end;

// Example 4: Get readable condition function display
var
  conditions: IwbContainer;
  i, count: integer;
  functionDisplay, typeDisplay: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      count := ElementCount(conditions);
      AddMessage(Format('Condition display values (%d total):', [count]));

      for i := 0 to count - 1 do begin
        // GetElementValues returns human-readable decoded strings
        functionDisplay := GetElementValues(e,
          Format('Conditions\[%d]\CTDA\Function', [i]));
        typeDisplay := GetElementValues(e,
          Format('Conditions\[%d]\CTDA\Type', [i]));

        AddMessage(Format('  [%d] %s (%s)', [i, functionDisplay, typeDisplay]));
      end;
    end;
  end;
end;
```

## See Also

- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [GetElementNativeValues](IwbContainer_GetElementNativeValues.md)
- [GetValue](IwbElement_GetValue.md)


