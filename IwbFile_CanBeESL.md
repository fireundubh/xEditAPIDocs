# CanBeESL

## Syntax

```pascal
function CanBeESL(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile`'s current load-order slot is a light slot.

This is the same check as [CanBeLight](IwbFile_CanBeLight.md) and [CanBeSmall](IwbFile_CanBeSmall.md). It does not read the header flag and it does not test whether the file's records would fit in a light plugin. [GetIsESL](IwbFile_GetIsESL.md) reads the flag.

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
  if Assigned(f) and CanBeESL(f) then
    AddMessage(GetFileName(f) + ' is in a light slot');
end;
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [CanBeSmall](IwbFile_CanBeSmall.md)
- [GetIsESL](IwbFile_GetIsESL.md)
- [SetIsESL](IwbFile_SetIsESL.md)
