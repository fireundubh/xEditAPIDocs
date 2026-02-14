# GetMasters

## Syntax

```pascal
procedure GetMasters(AFile: IwbFile; AFileNames: TStrings);
```

## Description

Populates `AFileNames` with master file names from `AFile`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to retrieve master file names from |
| AFileNames | TStrings | The string list to populate with master file names |

## Example

```pascal
l := TStringList.Create;
f := FileByName('SourceMod.esp');
GetMasters(f, l);
```

## See Also

- [AddMasterIfMissing](IwbFile_AddMasterIfMissing.md)
- [AddMasters](IwbFile_AddMasters.md)


