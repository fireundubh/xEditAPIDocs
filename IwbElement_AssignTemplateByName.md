# AssignTemplateByName

## Syntax

```pascal
function AssignTemplateByName(AElement: IwbElement; AElementIndex: Integer; ATemplateName: String): IInterface;
```

## Description

Returns a template element for `AElement` at `AElementIndex` by `ATemplateName`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the template from |
| AElementIndex | Integer | The index of the element to retrieve the template for |
| ATemplateName | String | The name of the template to assign |

## Returns

Returns the template element as an IInterface.

## Example

```pascal
// Example 1: Assign template by name at index
var
  container: IwbContainer;
  template: IInterface;
  templateElement: IwbElement;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'Conditions');
    if Assigned(container) then begin
      template := AssignTemplateByName(container, 0, 'Condition');
      if Assigned(template) then begin
        templateElement := template;
        SetToDefault(templateElement);
        AddMessage(Format('Assigned Condition template at index 0 in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Add multiple templates by name
var
  effects: IwbContainer;
  i: integer;
  template: IInterface;
  effectElement: IwbElement;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      for i := 0 to 2 do begin
        template := AssignTemplateByName(effects, i, 'Effect');
        if Assigned(template) then begin
          effectElement := template;
          SetToDefault(effectElement);
        end;
      end;
      AddMessage(Format('Added 3 Effect templates to %s', [EditorID(e)]));
    end;
  end;
end;

// Example 3: Conditional template assignment
var
  items: IwbContainer;
  template: IInterface;
  itemElement: IwbElement;
  templateCount: integer;
begin
  if Assigned(e) then begin
    items := ElementByPath(e, 'Items');
    if Assigned(items) then begin
      templateCount := AssignTemplateCount(items, 0);
      if templateCount > 0 then begin
        template := AssignTemplateByName(items, 0, 'Item');
        if Assigned(template) then begin
          itemElement := template;
          SetToDefault(itemElement);
          AddMessage(Format('Assigned Item template in %s', [EditorID(e)]));
        end;
      end else
        AddMessage('No templates available for Items');
    end;
  end;
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
