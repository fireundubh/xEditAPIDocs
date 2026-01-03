# AddMasters

## Syntax

```pascal
procedure AddMasters(AFile: IwbFile; AFileNames: TStrings);
```

## Description

Adds master files matching file names in `AFileNames` to `AFile`

## Example

```pascal
l := TStringList.Create;
f := FileByName('SourceMod.esp');
GetMasters(f, l);
o := FileByName('TargetMod.esp');
AddMasters(o, l);
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [GetMasters](IwbFile_GetMasters.md)


