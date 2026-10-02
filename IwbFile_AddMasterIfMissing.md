# AddMasterIfMissing

## Syntax

```pascal
procedure AddMasterIfMissing(AFile: IwbFile; AFileName: string; ASortMasters: Boolean = True; ASilent: Boolean = False);
```

## Description

Adds `AFileName` to `AFile`'s master list when that name is not already a master.

The file must already be loaded. If it is not, the call raises. Masters of the added file are added as well when the game requires them.

`ASortMasters` sorts the master list by the current load order after the add. Omitted, it is `True`. `ASilent` suppresses the messages the add would otherwise write. Omitted, it is `False`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to add the master to |
| AFileName | string | File name of a loaded file |
| ASortMasters | Boolean | Sort the master list by load order after adding. Defaults to `True` |
| ASilent | Boolean | Suppress messages. Defaults to `False` |

## Returns

Returns nothing.

## Example

```pascal
var
  targetFile: IwbFile;
begin
  targetFile := FileByIndex(0);
  if Assigned(targetFile) then begin
    AddMasterIfMissing(targetFile, 'Skyrim.esm');
    AddMasterIfMissing(targetFile, 'Update.esm', True, True);
  end;
end;
```

## See Also

- [AddMasters](IwbFile_AddMasters.md)
- [AddMastersIfMissing](IwbFile_AddMastersIfMissing.md)
- [GetMasters](IwbFile_GetMasters.md)
- [HasMaster](IwbFile_HasMaster.md)
- [SortMasters](IwbFile_SortMasters.md)
