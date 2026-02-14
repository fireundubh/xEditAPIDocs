# GetIsLight

## Syntax

```pascal
function GetIsLight(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Light file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it is Light |

## Returns

Returns `True` if the file is Light, `False` otherwise.

## Example

```pascal
if GetIsLight(f) then
  AddMessage(GetFileName(f) + ' is light');
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
- [GetIsESL](IwbFile_GetIsESL.md)
