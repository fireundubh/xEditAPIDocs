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

- [AddMasterIfMissing - IwbFile](IwbFile_AddMasterIfMissing.md)
- [AddMasters - IwbFile](IwbFile_AddMasters.md)
- [CleanMasters - IwbFile](IwbFile_CleanMasters.md)
- [GetMasters - IwbFile](IwbFile_GetMasters.md)
- [HasMaster - IwbFile](IwbFile_HasMaster.md)
- [Master - IwbMainRecord](IwbMainRecord_Master.md)
- [MasterOrSelf - IwbMainRecord](IwbMainRecord_MasterOrSelf.md)
- [MasterCount - IwbFile](IwbFile_MasterCount.md)
- [SortMasters - IwbFile](IwbFile_SortMasters.md)
