# SortMasters

## Syntax

```pascal
procedure SortMasters(AFile: IwbFile);
```

## Description

Reorders `AFile`'s master list to match the current load order.

For Oblivion and later, FormIDs whose master index changed are updated. If the order does not change, the file is left as it is. A file that is not editable raises. A file that is not a plugin returns without sorting. The change is in memory until the file is saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file whose masters are sorted |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('MyMod.esp');
  if Assigned(f) then
    SortMasters(f);
end;
```

## See Also

- [CleanMasters](IwbFile_CleanMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [MasterByIndex](IwbFile_MasterByIndex.md)
