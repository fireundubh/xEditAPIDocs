# CanBeSmall

## Syntax

```pascal
function CanBeSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile`'s current load-order slot is a light slot.

This is the same check as [CanBeLight](IwbFile_CanBeLight.md) and [CanBeESL](IwbFile_CanBeESL.md). It does not read the header flag and it does not test whether the file's records would fit in a light plugin. [GetIsSmall](IwbFile_GetIsSmall.md) reads the flag.

A file that is not an `IwbFile` returns `False`. A file with no load-order slot raises.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose load-order slot is tested |

## Returns

`True` when the load-order slot is a light slot, `False` when it is not or when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and CanBeSmall(f) then
    AddMessage(GetFileName(f) + ' is in a light slot');
end;
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
