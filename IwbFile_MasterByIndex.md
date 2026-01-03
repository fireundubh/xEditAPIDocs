# MasterByIndex

## Syntax

```pascal
function MasterByIndex(AFile: IwbFile; AIndex: Integer): IwbFile;
```

## Description

Returns the master file at `AIndex` in the list of master files required by `AFile`

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


