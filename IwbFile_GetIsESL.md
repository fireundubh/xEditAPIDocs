# GetIsESL

## Syntax

```pascal
function GetIsESL(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is light.

[GetIsLight](IwbFile_GetIsLight.md) and [GetIsSmall](IwbFile_GetIsSmall.md) are the same check. In pseudo-light mode this is the pseudo-light state. Otherwise, when the game supports light plugins and `AFile` is a plugin, this is the header light flag. Otherwise it is `False`. It is not the load-order slot. [CanBeESL](IwbFile_CanBeESL.md) tests the slot.

Returns `False` when `AFile` is not a file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check |

## Returns

`True` when the check above matches, `False` when it does not or when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and GetIsESL(f) then
    AddMessage(GetFileName(f) + ' is light');
end;
```

## See Also

- [CanBeESL](IwbFile_CanBeESL.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsESL](IwbFile_SetIsESL.md)
