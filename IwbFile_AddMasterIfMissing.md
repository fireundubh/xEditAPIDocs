# AddMasterIfMissing

## Syntax

```pascal
procedure AddMasterIfMissing(AFile: IwbFile; AFileName: String; ASortMasters: Boolean = True);
```

## Description

Adds the master file whose file name matches `AFileName` to `AFile`, if that master file does not exist in `AFile`'s master files list

If `ASortMasters` is `True`, after appending the specified master file, **AddMasterIfMissing** sorts `AFile`'s master files list by the current load order; otherwise, the list will not be sorted.

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


