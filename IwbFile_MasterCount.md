# MasterCount

## Syntax

```pascal
function MasterCount(AFile: IwbFile): Integer;
```

## Description

Returns the total number of master files that this file depends on.

This function retrieves the MasterCount property with the True parameter (including self), which counts all master file entries in the file header. These are plugins that must be loaded before this file for FormID references to resolve correctly. Returns 0 for files with no masters or invalid inputs. Use with MasterByIndex to iterate through all masters. The master list order matters for FormID resolution.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to count master files for |

## Returns

Returns the number of master files required by the file.

## Example

```pascal
for i := 0 to Pred(MasterCount(e)) do
  f := MasterByIndex(e, i);
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMasters](IwbFile_AddMasters.md)
- [CleanMasters](IwbFile_CleanMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [HasMaster](IwbFile_HasMaster.md)
- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [SortMasters](IwbFile_SortMasters.md)


