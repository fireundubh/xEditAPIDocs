# SetIsSmall

## Syntax

```pascal
procedure SetIsSmall(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Small file.

## Example

```pascal
if CanBeSmall(f) then
  SetIsSmall(f, True);
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
