# CleanMasters

## Syntax

```pascal
procedure CleanMasters(AFile: IwbFile);
```

## Description

Removes master file entries that are not referenced by any records in the file.

This function calls the file's CleanMasters method, which scans all records to identify which masters are actually used and removes unused entries from the master list. This reduces the file's dependency footprint and can resolve load order conflicts. The operation may be slow for large files. Master order is preserved for remaining masters. Changes take effect immediately but must be saved to persist.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to clean master files from |

## Example

```pascal
f := FileByName('MyMod.esp');
CleanMasters(f);
```

## See Also

- [HasMaster](IwbFile_HasMaster.md)
- [MasterCount](IwbFile_MasterCount.md)
- [SortMasters](IwbFile_SortMasters.md)


