# SortMasters

## Syntax

```pascal
procedure SortMasters(AFile: IwbFile);
```

## Description

Reorders the master file list to match the current load order sequence.

This function calls the file's SortMasters method, which sorts the master list entries based on their current load order positions. After sorting, all FormID references are updated to reflect the new master indices, and affected records are marked as modified. Essential after adding masters or when load order has changed. The operation ensures FormID references remain valid after the master list is reordered. May be slow for files with many records.

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


