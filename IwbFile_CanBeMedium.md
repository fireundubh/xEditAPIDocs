# CanBeMedium

## Syntax

```pascal
function CanBeMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Medium file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it can be Medium |

## Returns

Returns `True` if the file can be Medium, `False` otherwise.

## Example

```pascal
if CanBeMedium(f) then
  SetIsMedium(f, True);
```

## See Also

- [GetIsMedium](IwbFile_GetIsMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
