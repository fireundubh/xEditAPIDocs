# HasMaster

## Syntax

```pascal
function HasMaster(AFile: IwbFile; AFileName: string): Boolean;
```

## Description

Returns whether `AFile`'s current master list contains `AFileName`.

The name comparison is case-insensitive. This does not test whether that master is loaded in the session.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose masters are searched |
| AFileName | string | Master file name to look for |

## Returns

`True` when a master has that name, `False` when none does. If `AFile` is not a file, the result is unassigned.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('Dawnguard.esm');
  if Assigned(f) and HasMaster(f, 'Skyrim.esm') then
    AddMessage('Dawnguard.esm masters Skyrim.esm');
end;
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [GetMasters](IwbFile_GetMasters.md)
- [MasterCount](IwbFile_MasterCount.md)
