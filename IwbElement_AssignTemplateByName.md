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
var
  t: IInterface;
begin
  t := AssignTemplateByName(e, 0, 'SomeTemplate');
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateCount](IwbElement_AssignTemplateCount.md)
