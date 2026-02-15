# ShortName

## Syntax

```pascal
function TemplateAssign(AElement: IwbElement; ATemplateName: string): IwbElement;
```

## Description

Assigns a template by name to an element and returns that new element

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element that will receive the template |
| ATemplateName | string | The name of the template (assumed to be unique) |

## Returns

Returns the newly created element as an IwbElement interface.

## Example

```pascal
// Example 1: Assign condition template
var
  conditions: IwbElement;
  newCondition: IwbElement;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      newCondition := TemplateAssign(conditions, 'Condition');
      if Assigned(newCondition) then begin
        SetElementEditValue(newCondition, 'CTDA\Function', 'GetItemCount');
        SetElementEditValue(newCondition, 'CTDA\Comparison Value', '1');
        AddMessage(Format('Added condition to %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Assign menu item template
var
  menuItems: IwbElement;
  newMenuItem: IwbElement;
begin
  if Assigned(e) then begin
    menuItems := ElementByPath(e, 'Menu Items');
    if Assigned(menuItems) then begin
      newMenuItem := TemplateAssign(menuItems, 'Menu Item');
      if Assigned(newMenuItem) then begin
        SetElementEditValue(newMenuItem, 'INAM', 'New Item');
        AddMessage(Format('Added menu item to %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 3: Assign multiple templates
var
  effects: IwbElement;
  i: integer;
  newEffect: IwbElement;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      for i := 0 to 2 do begin
        newEffect := TemplateAssign(effects, 'Effect');
        if Assigned(newEffect) then begin
          SetElementEditValue(newEffect, 'EFID', '00012345');
          SetElementEditValue(newEffect, 'EFIT\Magnitude', IntToStr((i + 1) * 10));
        end;
      end;
      AddMessage(Format('Added 3 effects to %s', [EditorID(e)]));
    end;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [DisplayName](IwbElement_DisplayName.md)
- [PathName](IwbElement_PathName.md)


