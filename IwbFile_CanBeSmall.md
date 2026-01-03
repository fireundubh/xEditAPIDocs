# CanBeSmall

## Syntax

```pascal
function CanBeSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Small file.

## Example

```pascal
if CanBeSmall(f) then
  SetIsSmall(f, True);
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
