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
var
  element: IwbElement;
  oldValue, newValue: string;
begin
  element := ElementByPath(e, 'EDID');
  oldValue := GetEditValue(element);
  newValue := SetEditValue(element, 'MyNewEditorID');
  AddMessage('Changed value from "' + oldValue + '" to "' + newValue + '"');
end;
```

## See Also

- [GetEditValue](IwbElement_GetEditValue.md)
- [SetNativeValue](IwbElement_SetNativeValue.md)
- [GetNativeValue](IwbElement_GetNativeValue.md)
- [GetValue](IwbElement_GetValue.md)
- [SetElementEditValues](IwbContainer_SetElementEditValues.md)
- [IsEditable](IwbElement_IsEditable.md)


