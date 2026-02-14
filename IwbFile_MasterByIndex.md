# MasterByIndex

## Syntax

```pascal
function MasterByIndex(AFile: IwbFile; AIndex: Integer): IwbFile;
```

## Description

Returns the master file at the specified zero-based index in the master list.

This function accesses the Masters property by index with bounds checking. Returns the IwbFile interface for the master at that position in the file header's master list. Returns nil if the index is >= MasterCount. The order of masters in the list is significant for FormID reference resolution. Master 0 is always the first dependency.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to retrieve the master from |
| AIndex | Integer | The zero-based index of the master file in the master list |

## Returns

Returns the IwbFile interface for the master file at the specified index.

## Example

```pascal
f := FileByName('Dawnguard.esm');
m := MasterByIndex(f, 0);  // Skyrim.esm
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMasters](IwbFile_AddMasters.md)
- [CleanMasters](IwbFile_CleanMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [HasMaster](IwbFile_HasMaster.md)
- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [MasterCount](IwbFile_MasterCount.md)
- [SortMasters](IwbFile_SortMasters.md)


