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
var
  t: IInterface;
begin
  t := AssignTemplateByIndex(e, 0, 1);
end;
```

## See Also

- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
