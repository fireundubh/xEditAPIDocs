# GetIsMedium

## Syntax

```pascal
function GetIsMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Medium file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it is Medium |

## Returns

Returns `True` if the file is Medium, `False` otherwise.

## Example

```pascal
if GetIsMedium(f) then
  AddMessage(GetFileName(f) + ' is medium');
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
