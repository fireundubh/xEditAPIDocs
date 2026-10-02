# CanBeLight

## Syntax

```pascal
function CanBeLight(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile`'s current load-order slot is a light slot.

This is the same check as [CanBeESL](IwbFile_CanBeESL.md) and [CanBeSmall](IwbFile_CanBeSmall.md). It does not read the header flag and it does not test whether the file's records would fit in a light plugin. [GetIsLight](IwbFile_GetIsLight.md) reads the flag.

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
  if Assigned(f) and CanBeLight(f) then
    AddMessage(GetFileName(f) + ' is in a light slot');
end;
```

## See Also

- [CanBeESL](IwbFile_CanBeESL.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
