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
var
  count: Integer;
begin
  count := AssignTemplateCount(e, 0);
end;
```

## See Also

- [AssignTemplateByIndex](IwbElement_AssignTemplateByIndex.md)
- [AssignTemplateByName](IwbElement_AssignTemplateByName.md)
