# AddMasterIfMissing

## Syntax

```pascal
procedure AddMasterIfMissing(AFile: IwbFile; AFileName: String; ASortMasters: Boolean = True);
```

## Description

Adds a master file dependency to the file's header if not already present.

This function calls the AddMasterIfMissing method, which checks if the specified filename exists in the master list and adds it if missing. Optional parameters control sorting and additional behavior. The ASortMasters parameter (default true) determines whether to sort the master list by load order after adding. Adding masters is necessary before creating records that reference another file's content. The master file must be loaded in the current session.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to add the master to |
| AFileName | String | The name of the master file to add |
| ASortMasters | Boolean | If true, sorts the master files list by load order after adding (defaults to true) |

## Example

```pascal
var
  targetFile: IwbFile;
begin
  AddMasterIfMissing(targetFile, 'Skyrim.esm');
  AddMasterIfMissing(targetFile, 'Skyrim.esm', True, True);
end;
```

## See Also

- [AddMasters](IwbFile_AddMasters.md)
- [GetMasters](IwbFile_GetMasters.md)
- [HasMaster](IwbFile_HasMaster.md)
- [SortMasters](IwbFile_SortMasters.md)


