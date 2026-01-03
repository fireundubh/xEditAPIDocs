# GetIsMedium

## Syntax

```pascal
function GetIsMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Medium file.

## Example

```pascal
if GetIsMedium(f) then
  AddMessage(GetFileName(f) + ' is medium');
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
