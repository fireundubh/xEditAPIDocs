# SetIsLight

## Syntax

```pascal
procedure SetIsLight(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Light file.

## Example

```pascal
if CanBeLight(f) then
  SetIsLight(f, True);
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsESL](IwbFile_SetIsESL.md)
