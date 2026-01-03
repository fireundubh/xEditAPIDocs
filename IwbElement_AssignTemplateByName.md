# AssignTemplateByName

## Syntax

```pascal
function AssignTemplateByName(AElement: IwbElement; AElementIndex: Integer; ATemplateName: String): IInterface;
```

## Description

Returns a template element for `AElement` at `AElementIndex` by `ATemplateName`.

## Example

```pascal
var
  t: IInterface;
begin
  t := AssignTemplateByName(e, 0, 'SomeTemplate');
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
