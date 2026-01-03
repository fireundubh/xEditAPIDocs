# GetFileName

## Syntax

```pascal
function GetFileName(AFile: IwbFile): String;
```

## Description

Returns the file name and extension for `AFile`

## Example

```pascal
f := FileByIndex(0);
sFileName := GetFileName(f);
AddMessage(sFileName);  // --> 'Skyrim.esm'
```

## See Also

- [FileByIndex](../Global/Global_FileByIndex.md)
- [FileByName](../Global/Global_FileByName.md)
- [GetFile](../IwbElement/IwbElement_GetFile.md)
