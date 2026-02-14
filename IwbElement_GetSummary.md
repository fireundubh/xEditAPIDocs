# GetSummary

## Syntax

```pascal
function GetSummary(AElement: IwbElement): String;
```

## Description

Returns a summary string for `AElement`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get a summary for |

## Returns

Returns a summary string describing the element.

## Example

```pascal
var
  element: IwbElement;
  summary: string;
begin
  element := ElementByPath(e, 'EDID');
  summary := GetSummary(element);
  AddMessage('Element summary: ' + summary);
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)
- [GetValue](IwbElement_GetValue.md)
