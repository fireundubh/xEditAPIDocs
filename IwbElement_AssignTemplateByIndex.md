# AssignTemplateByIndex

## Syntax

```pascal
function AssignTemplateByIndex(AElement: IwbElement; AElementIndex: Integer; ATemplateIndex: Integer): IInterface;
```

## Description

Returns a template element for `AElement` at `AElementIndex` by `ATemplateIndex`.

## Example

```pascal
var
  t: IInterface;
begin
  t := AssignTemplateByIndex(e, 0, 1);
end;
```

## See Also

- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
