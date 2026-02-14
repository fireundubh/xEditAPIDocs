# GetNewFormID

## Syntax

```pascal
function GetNewFormID(AFile: IwbFile): Cardinal;
```

## Description

Returns the next available Form ID relative to `AFile`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to get the next form ID for |

## Returns

Returns the next available form ID as a Cardinal value.

## Example

```pascal
var
    result: Cardinal;
begin
    result := GetNewFormID(f);
end;
```
