# GetIsLight

## Syntax

```pascal
function GetIsLight(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Light file.

## Example

```pascal
if GetIsLight(f) then
  AddMessage(GetFileName(f) + ' is light');
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
- [GetIsESL](IwbFile_GetIsESL.md)
