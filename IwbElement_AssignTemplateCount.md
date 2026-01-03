# AssignTemplateCount

## Syntax

```pascal
function AssignTemplateCount(AElement: IwbElement; AElementIndex: Integer): Integer;
```

## Description

Returns the number of assign templates for `AElement` at `AElementIndex`.

## Example

```pascal
var
  count: Integer;
begin
  count := AssignTemplateCount(e, 0);
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
