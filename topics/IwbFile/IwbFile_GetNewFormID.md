# GetNewFormID

## Syntax

```pascal
function GetNewFormID(AFile: IwbFile): Cardinal;
```

## Description

Returns the next available Form ID relative to `AFile`

## Example

```pascal
var
    result: Cardinal;
begin
    result := GetNewFormID(f);
end;
```