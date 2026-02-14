# SortMasters

## Syntax

```pascal
procedure SortMasters(AFile: IwbFile);
```

## Description

Sorts the master file list in `AFile`'s file header by the current load order. When the list is sorted, references to the affected masters are updated and affected records are marked as modified.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose master list should be sorted |

## Example

```pascal
f := FileByName('MyMod.esp');
SortMasters(f);
```

## See Also

- [CleanMasters](IwbFile_CleanMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [MasterByIndex](IwbFile_MasterByIndex.md)


