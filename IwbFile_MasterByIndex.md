# MasterByIndex

## Syntax

```pascal
function MasterByIndex(AFile: IwbFile; AIndex: Integer): IwbFile;
```

## Description

Returns the master at `AIndex` in `AFile`'s current master list.

The index is zero-based. Master 0 is the first dependency. The list is the one after any masters added, removed, or sorted in this session. It does not include `AFile` itself.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose masters are indexed |
| AIndex | Integer | Zero-based index, from 0 through `MasterCount(AFile) - 1` |

## Returns

The master file at that index. The result is unassigned when `AIndex` is negative, `AIndex` is not less than [MasterCount](IwbFile_MasterCount.md), or `AFile` is not a file.

## Example

```pascal
var
  f, m: IwbFile;
begin
  f := FileByName('Dawnguard.esm');
  if Assigned(f) then begin
    m := MasterByIndex(f, 0);
    if Assigned(m) then
      AddMessage(GetFileName(m));
  end;
end;
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [CleanMasters](IwbFile_CleanMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [HasMaster](IwbFile_HasMaster.md)
- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [MasterCount](IwbFile_MasterCount.md)
- [SortMasters](IwbFile_SortMasters.md)
