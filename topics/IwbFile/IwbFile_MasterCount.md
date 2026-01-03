# MasterCount

## Syntax

```pascal
function MasterCount(AFile: IwbFile): Integer;
```

## Description

Returns the number of master files required by `AFile`

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
- [Master](../IwbMainRecord/IwbMainRecord_Master.md)
- [MasterOrSelf](../IwbMainRecord/IwbMainRecord_MasterOrSelf.md)
- [SortMasters](IwbFile_SortMasters.md)
