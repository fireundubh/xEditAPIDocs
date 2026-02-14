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
AddMessage(GetSummary(e));
```
