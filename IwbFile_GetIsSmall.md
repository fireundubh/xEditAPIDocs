# GetIsSmall

## Syntax

```pascal
function GetIsSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Small file.

## Example

```pascal
if GetIsSmall(f) then
  AddMessage(GetFileName(f) + ' is small');
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
