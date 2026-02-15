# GetValue

## Syntax

```pascal
function GetValue(AElement: IwbElement): string;
```

## Description

Returns the string display value of an element as it is displayed in the UI. This provides the formatted, human-readable representation of the element's value, useful for things like decoded texture hashes, localized strings, and other display-specific formatting.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose display value to retrieve |

## Returns

Returns a string containing the formatted display value of the element as it appears in the xEdit UI.

## Example

```pascal
// Example 1: Get UI-formatted value
var
  element: IwbElement;
  displayValue: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'EDID');
    if Assigned(element) then begin
      displayValue := GetValue(element);
      AddMessage(Format('Editor ID (UI format): %s', [displayValue]));
    end;
  end;
end;

// Example 2: Compare GetValue vs GetEditValue
var
  element: IwbElement;
  displayValue, editValue: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'NAME');
    if Assigned(element) then begin
      displayValue := GetValue(element);
      editValue := GetEditValue(element);
      AddMessage('Display value: ' + displayValue);
      AddMessage('Edit value: ' + editValue);
      // Display might include resolved record name, edit is just FormID
    end;
  end;
end;

// Example 3: Log formatted values for reporting
var
  container: IwbContainer;
  i: integer;
  element: IwbElement;
  name, displayValue: string;
begin
  if Assigned(e) then begin
    container := e;
    AddMessage(Format('Display values for %s:', [EditorID(e)]));
    for i := 0 to ElementCount(container) - 1 do begin
      element := ElementByIndex(container, i);
      if Assigned(element) then begin
        name := Name(element);
        displayValue := GetValue(element);
        if displayValue <> '' then
          AddMessage(Format('  %s = %s', [name, displayValue]));
      end;
    end;
  end;
end;
```

## See Also

- [GetEditValue](IwbElement_GetEditValue.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [SetEditValue](IwbElement_SetEditValue.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetElementValues](IwbContainer_GetElementValues.md)


