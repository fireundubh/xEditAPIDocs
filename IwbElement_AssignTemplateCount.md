# AssignTemplateCount

## Syntax

```pascal
function AssignTemplateCount(AElement: IwbElement; AElementIndex: Integer): Integer;
```

## Description

Returns the number of assign templates for `AElement` at `AElementIndex`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to count templates for |
| AElementIndex | Integer | The index of the element to count templates for |

## Returns

Returns the number of assign templates as an Integer.

## Example

```pascal
// Example 1: Check template availability
var
  conditions: IwbContainer;
  templateCount: integer;
begin
  if Assigned(e) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      templateCount := AssignTemplateCount(conditions, 0);
      if templateCount > 0 then
        AddMessage(Format('Conditions has %d available template(s)', [templateCount]))
      else
        AddMessage('No templates available for Conditions');
    end;
  end;
end;

// Example 2: List all available templates
var
  effects: IwbContainer;
  i, templateCount: integer;
  template: IInterface;
  templateElement: IwbElement;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      templateCount := AssignTemplateCount(effects, 0);
      AddMessage(Format('Effects has %d template(s):', [templateCount]));
      for i := 0 to templateCount - 1 do begin
        template := AssignTemplateByIndex(effects, 0, i);
        if Assigned(template) then begin
          templateElement := template;
          AddMessage(Format('  [%d] %s', [i, Name(templateElement)]));
        end;
      end;
    end;
  end;
end;

// Example 3: Validate before template assignment
var
  items: IwbContainer;
  templateCount: integer;
  template: IInterface;
  itemElement: IwbElement;
begin
  if Assigned(e) then begin
    items := ElementByPath(e, 'Items');
    if Assigned(items) then begin
      templateCount := AssignTemplateCount(items, 0);
      if templateCount > 0 then begin
        template := AssignTemplateByIndex(items, 0, 0);
        if Assigned(template) then begin
          itemElement := template;
          SetToDefault(itemElement);
          AddMessage(Format('Assigned first of %d templates', [templateCount]));
        end;
      end else
        AddMessage(Format('Cannot add items to %s - no templates defined', [EditorID(e)]));
    end;
  end;
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
