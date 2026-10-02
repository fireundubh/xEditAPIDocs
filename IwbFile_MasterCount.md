# MasterCount

## Syntax

```pascal
function MasterCount(AFile: IwbFile): Integer;
```

## Description

Returns how many masters `AFile` currently has.

The count is the master list after any masters added, removed, or sorted in this session. `AFile` itself is not included. Pair it with [MasterByIndex](IwbFile_MasterByIndex.md).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose masters are counted |

## Returns

The number of masters, or `0` when `AFile` is not a file.

## Example

```pascal
var
  f, m: IwbFile;
  i: Integer;
begin
  f := FileByName('Dawnguard.esm');
  if Assigned(f) then
    for i := 0 to Pred(MasterCount(f)) do begin
      m := MasterByIndex(f, i);
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
- [MasterByIndex](IwbFile_MasterByIndex.md)
- [SortMasters](IwbFile_SortMasters.md)
