# CleanMasters

## Syntax

```pascal
procedure CleanMasters(AFile: IwbFile);
```

## Description

Removes master entries that no record in `AFile` references. For Oblivion and later, FormIDs whose master index changed are updated.

The game master stays even when nothing references it. If the session requires every master of a used master, those stay too. Remaining masters keep their relative order. The change is in memory until the file is saved. Large files can take a while.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose master list is cleaned |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) then
    CleanMasters(f);
end;
```

## See Also

- [HasMaster](IwbFile_HasMaster.md)
- [MasterCount](IwbFile_MasterCount.md)
- [SortMasters](IwbFile_SortMasters.md)
