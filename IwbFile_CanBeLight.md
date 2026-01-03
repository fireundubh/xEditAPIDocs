# CanBeLight

## Syntax

```pascal
function CanBeLight(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Light file.

## Example

```pascal
if CanBeLight(f) then
  SetIsLight(f, True);
```

## See Also

- [CanBeESL](IwbFile_CanBeESL.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
