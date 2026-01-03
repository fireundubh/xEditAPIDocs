# ShortName

## Syntax

```pascal
function TemplateAssign(AElement: IwbElement; ATemplateName: string): IwbElement;
```

## Description

Assigns a template by name to an element and returns that new element

Parameters:

- `AElement`: the element that will receive the template
- `ATemplateName`: the name of the template (assumed to be unique)

## Example

```pascal
var
    targetElement: IwbElement;
    targetCondition: IwbElement;
begin
    targetElement := ElementByPath(e, 'Menu Items\[0]\Conditions');
    targetCondition := TemplateAssign(targetElement, 'Condition');
    // do stuff
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [BaseName](IwbElement_BaseName.md)
- [DisplayName](IwbElement_DisplayName.md)
- [PathName](IwbElement_PathName.md)


