# CleanMasters

## Syntax

```pascal
procedure CleanMasters(AFile: IwbFile);
```

## Description

Removes unused master files from `AFile`'s master files list

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


