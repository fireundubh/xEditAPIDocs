# SetEditValue

## Syntax

```pascal
procedure SetEditValue(AElement: IwbElement; AValue: string);
```

## Description

Sets the element's value using a human-readable string representation.

This function assigns to the EditValue property, which parses the string and converts it to the appropriate internal format based on the element's definition type. The element must be editable for this operation to succeed. Invalid strings may raise an exception or fail silently depending on the element type.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to set the value for |
| AValue | string | The new value as a string |

## Returns

This procedure does not return a value.

## Example

```pascal
// Example 1: Rename a record's Editor ID
var
  edidElement: IwbElement;
  oldValue: string;
begin
  if Assigned(e) then begin
    edidElement := ElementByPath(e, 'EDID');
    if Assigned(edidElement) then begin
      oldValue := GetEditValue(edidElement);
      SetEditValue(edidElement, 'MyNewEditorID');
      AddMessage(Format('Changed Editor ID from "%s" to "%s"', [oldValue, GetEditValue(edidElement)]));
    end;
  end;
end;

// Example 2: Batch update multiple elements
var
  fullElement, valueElement: IwbElement;
begin
  if Assigned(e) then begin
    BeginUpdate(e);
    try
      fullElement := ElementByPath(e, 'DATA\Full');
      if Assigned(fullElement) then
        SetEditValue(fullElement, 'New Display Name');

      valueElement := ElementByPath(e, 'DATA\Value');
      if Assigned(valueElement) then
        SetEditValue(valueElement, '100');
    finally
      EndUpdate(e);
    end;
  end;
end;

// Example 3: Set FormID reference
var
  baseElement: IwbElement;
  targetFormID: string;
begin
  if Assigned(e) then begin
    baseElement := ElementByPath(e, 'NAME');
    if Assigned(baseElement) then begin
      targetFormID := '00012E46'; // Iron Armor
      SetEditValue(baseElement, targetFormID);
      AddMessage('Set base object to FormID: ' + targetFormID);
    end;
  end;
end;
```

## See Also

- [GetEditValue](IwbElement_GetEditValue.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [GetValue](IwbElement_GetValue.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
- [IsEditable](IwbElement_IsEditable.md)


