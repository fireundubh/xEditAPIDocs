# GetIsSmall

## Syntax

```pascal
function GetIsSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is light.

There is no separate small-plugin flag. [GetIsLight](IwbFile_GetIsLight.md) and [GetIsESL](IwbFile_GetIsESL.md) are the same check. In pseudo-light mode this is the pseudo-light state. Otherwise, when the game supports light plugins and `AFile` is a plugin, this is the header light flag. Otherwise it is `False`. [CanBeSmall](IwbFile_CanBeSmall.md) tests the load-order slot, not this value.

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
  if Assigned(f) and GetIsSmall(f) then
    AddMessage(GetFileName(f) + ' is light');
end;
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
