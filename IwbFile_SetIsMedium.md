# SetIsMedium

## Syntax

```pascal
procedure SetIsMedium(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Medium file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to set the Medium flag on |
| AValue | Boolean | Whether to set (True) or clear (False) the Medium flag |

## Example

```pascal
if CanBeMedium(f) then
  SetIsMedium(f, True);
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [GetIsMedium](IwbFile_GetIsMedium.md)
