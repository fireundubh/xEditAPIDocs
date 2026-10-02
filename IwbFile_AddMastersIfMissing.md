# AddMastersIfMissing

## Syntax

```pascal
procedure AddMastersIfMissing(AFile: IwbFile; AMasters: TStrings; ASortMasters: Boolean = True; ASilent: Boolean = False);
```

## Description

Adds the master files whose file names are in `AMasters` to `AFile`, if those names are not already masters.

Each name must already be loaded. If one is not, the call raises. Masters of an added file are added as well when the game requires them.

If `ASortMasters` is `True`, the master list is sorted by the current load order after the add. Omitted, it is `True`.

If `ASilent` is `True`, messages from the add are suppressed. Omitted, it is `False`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to add the masters to |
| AMasters | TStrings | Master file names to add |
| ASortMasters | Boolean | Sort the master list by load order after adding. Defaults to `True` |
| ASilent | Boolean | Suppress messages. Defaults to `False` |

## Returns

Returns nothing.

## Example

```pascal
var
  targetFile: IwbFile;
  masterList: TStringList;
begin
  targetFile := FileByIndex(0);
  if Assigned(targetFile) then begin
    masterList := TStringList.Create;
    try
      masterList.Add('Skyrim.esm');
      masterList.Add('Update.esm');
      AddMastersIfMissing(targetFile, masterList);
      AddMastersIfMissing(targetFile, masterList, True, True);
    finally
      masterList.Free;
    end;
  end;
end;
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMasters](IwbFile_AddMasters.md)
- [ReportRequiredMasters](IwbElement_ReportRequiredMasters.md)
