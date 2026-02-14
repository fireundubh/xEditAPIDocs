# AddMastersIfMissing

## Syntax

```pascal
procedure AddMastersIfMissing(AFile: IwbFile; AMasters: TStrings; ASortMasters: boolean = True; ASilent: boolean = False);
```

## Description

Adds the master files whose file names are provided in `AMasters` to `AFile`, if those master files do not exist in `AFile`'s master files list.

If `ASortMasters` is `True`, after appending the specified master files, **AddMastersIfMissing** sorts `AFile`'s master files list by the current load order; otherwise, the list will not be sorted.

If `ASilent` is `True`, **AddMastersIfMissing** will not display any message notifications during the process.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to add the masters to |
| AMasters | TStrings | The list of master file names to add |
| ASortMasters | boolean | If true, sorts the master files list by load order after adding (defaults to true) |
| ASilent | boolean | If true, suppresses message notifications (defaults to false) |

## Example

```pascal
var
  targetFile: IwbFile;
  masterList: TStringList;
begin
  masterList := TStringList.Create;
  masterList.Add('Skyrim.esm');
  masterList.Add('Update.esm');
  masterList.Add('Dragonborn.esm');

  AddMastersIfMissing(targetFile, masterList);
  AddMastersIfMissing(targetFile, masterList, True, True);

  masterList.Free;
end;
```

## See Also

- [AddMasterIfMissing - IwbFile](IwbFile_AddMasterIfMissing.md)
- [ReportRequiredMasters - IwbElement](IwbElement_ReportRequiredMasters.md)


