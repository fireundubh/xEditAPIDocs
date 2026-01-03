# SetIsMedium

## Syntax

```pascal
procedure SetIsMedium(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Medium file.

## Example

```pascal
if CanBeMedium(f) then
  SetIsMedium(f, True);
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [GetIsMedium](IwbFile_GetIsMedium.md)
