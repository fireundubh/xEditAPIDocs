# AssignTemplateByIndex

## Syntax

```pascal
function AssignTemplateByIndex(AElement: IwbElement; AElementIndex: Integer; ATemplateIndex: Integer): IInterface;
```

## Description

Returns a template element for `AElement` at `AElementIndex` by `ATemplateIndex`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the template from |
| AElementIndex | Integer | The index of the element to retrieve the template for |
| ATemplateIndex | Integer | The index of the template to assign |

## Returns

Returns the template element as an IInterface.

## Example

```pascal
// Example 1: Assign template by index
var
  container: IwbContainer;
  template: IInterface;
  templateElement: IwbElement;
begin
  if Assigned(e) then begin
    container := ElementByPath(e, 'Conditions');
    if Assigned(container) then begin
      template := AssignTemplateByIndex(container, 0, 0);
      if Assigned(template) then begin
        templateElement := template;
        SetToDefault(templateElement);
        AddMessage(Format('Assigned template index 0 at element 0 in %s', [EditorID(e)]));
      end;
    end;
  end;
end;

// Example 2: Iterate through available templates
var
  effects: IwbContainer;
  i, templateCount: integer;
  template: IInterface;
  effectElement: IwbElement;
begin
  if Assigned(e) then begin
    effects := ElementByPath(e, 'Effects');
    if Assigned(effects) then begin
      templateCount := AssignTemplateCount(effects, 0);
      if templateCount > 0 then begin
        AddMessage(Format('Found %d templates for Effects', [templateCount]));
        for i := 0 to templateCount - 1 do begin
          template := AssignTemplateByIndex(effects, i, i);
          if Assigned(template) then begin
            effectElement := template;
            AddMessage(Format('  Template %d: %s', [i, Name(effectElement)]));
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Assign specific template variant
var
  items: IwbContainer;
  template: IInterface;
  itemElement: IwbElement;
  templateIdx: integer;
begin
  if Assigned(e) then begin
    items := ElementByPath(e, 'Items');
    if Assigned(items) then begin
      // Use template at index 2 (third variant)
      templateIdx := 2;
      if AssignTemplateCount(items, 0) > templateIdx then begin
        template := AssignTemplateByIndex(items, 0, templateIdx);
        if Assigned(template) then begin
          itemElement := template;
          SetToDefault(itemElement);
          AddMessage(Format('Assigned template variant %d in %s',
            [templateIdx, EditorID(e)]));
        end;
      end else
        AddMessage('Template index out of range');
    end;
  end;
end;
```

## See Also

- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
