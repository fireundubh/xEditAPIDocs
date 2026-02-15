# GetEditValue

## Syntax

```pascal
function GetEditValue(AElement: IwbElement): string;
```

## Description

Returns the element's value as a human-readable and editable string representation.

This function retrieves the EditValue property, which provides a formatted string suitable for display and editing in user interfaces. The format depends on the element's definition type (e.g., integers as decimal strings, FormIDs as hex strings, enums as their names). Returns an empty string if the element is invalid.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the edit value from |

## Returns

Returns the element's edit value as a string.

## Example

```pascal
// Example 1: Get edit value from a specific element
var
  edidElement: IwbElement;
  editorID: string;
begin
  if Assigned(e) then begin
    edidElement := ElementByPath(e, 'EDID');
    if Assigned(edidElement) then begin
      editorID := GetEditValue(edidElement);
      AddMessage('Editor ID: ' + editorID);
    end;
  end;
end;

// Example 2: Read FormID as hex string
var
  baseElement: IwbElement;
  formIDHex: string;
begin
  if Assigned(e) then begin
    baseElement := ElementByPath(e, 'NAME');
    if Assigned(baseElement) then begin
      formIDHex := GetEditValue(baseElement);
      AddMessage('Base Object FormID: ' + formIDHex);
    end;
  end;
end;

// Example 3: Iterate array and read values
var
  conditions: IwbContainer;
  i: integer;
  condition: IwbElement;
  funcValue: string;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      for i := 0 to ElementCount(conditions) - 1 do begin
        condition := ElementByIndex(conditions, i);
        funcValue := GetEditValue(ElementByPath(condition, 'CTDA\Function'));
        AddMessage(Format('Condition %d Function: %s', [i, funcValue]));
      end;
    end;
  end;
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetValue](IwbElement_GetValue.md)
- [GetElementEditValues](IwbContainer_GetElementEditValues.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)


