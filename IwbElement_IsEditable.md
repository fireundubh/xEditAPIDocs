# IsEditable

## Syntax

```pascal
function IsEditable(AElement: IwbElement): boolean;
```

## Description

Checks if an element can be edited.

Returns true if the element can be modified. Some elements, particularly those in base game master files like Skyrim.esm, may be locked from editing.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check if it's editable |

## Returns

Returns true if the element can be edited, false otherwise.

## Example

```pascal
var
  canEdit: boolean;
begin
  if IsEditable(element) then
    SetEditValue(element, 'New Value');
end;
```

## See Also

- [SetEditValue](IwbElement_SetEditValue.md)
- [SetElementState](IwbElement_SetElementState.md)


