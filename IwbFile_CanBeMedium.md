# CanBeMedium

## Syntax

```pascal
function CanBeMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile`'s current load-order slot is a medium slot.

It does not read the header flag and it does not test whether the file's records would fit in a medium plugin. [GetIsMedium](IwbFile_GetIsMedium.md) reads the flag.

A file that is not an `IwbFile` returns `False`. A file with no load-order slot raises.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose load-order slot is tested |

## Returns

`True` when the load-order slot is a medium slot, `False` when it is not or when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and CanBeMedium(f) then
    AddMessage(GetFileName(f) + ' is in a medium slot');
end;
```

## See Also

- [GetIsMedium](IwbFile_GetIsMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
