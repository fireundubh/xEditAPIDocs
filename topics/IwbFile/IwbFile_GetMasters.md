# GetMasters

## Syntax

```pascal
procedure GetMasters(AFile: IwbFile; AFileNames: TStrings);
```

## Description

Populates `AFileNames` with master file names from `AFile`

## Example

```pascal
l := TStringList.Create;
f := FileByName('SourceMod.esp');
GetMasters(f, l);
```

## See Also

- [AddMasterIfMissing](../IwbFile/IwbFile_AddMasterIfMissing.md)
- [AddMasters](../IwbFile/IwbFile_AddMasters.md)
