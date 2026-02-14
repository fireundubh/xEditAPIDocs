# AddMasters

## Syntax

```pascal
procedure AddMasters(AFile: IwbFile; AFileNames: TStrings);
```

## Description

Adds multiple master files to a plugin file. All file names in the `AFileNames` string list will be added as masters to `AFile`. This is useful when copying records or references between files that require specific masters.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to which masters will be added |
| AFileNames | TStrings | A string list containing the file names of masters to add |

## Returns

This function does not return a value.

## Example

```pascal
var
  sourceFile, targetFile: IwbFile;
  masterList: TStringList;
begin
  masterList := TStringList.Create;
  try
    sourceFile := FileByName('SourceMod.esp');
    GetMasters(sourceFile, masterList);

    targetFile := FileByName('TargetMod.esp');
    AddMasters(targetFile, masterList);

    AddMessage('Added ' + IntToStr(masterList.Count) + ' masters to ' + GetFileName(targetFile));
  finally
    masterList.Free;
  end;
end;
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMastersIfMissing](IwbFile_AddMastersIfMissing.md)
- [GetMasters](IwbFile_GetMasters.md)
- [CleanMasters](IwbFile_CleanMasters.md)


