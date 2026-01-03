# CanBeMedium

## Syntax

```pascal
function CanBeMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Medium file.

## Example

```pascal
if CanBeMedium(f) then
  SetIsMedium(f, True);
```

## See Also

- [GetIsMedium](IwbFile_GetIsMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
