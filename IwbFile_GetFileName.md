# GetFileName

## Syntax

```pascal
function GetFileName(AFile: IwbFile): String;
```

## Description

Returns the file name and extension for `AFile`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to get the name from |

## Returns

Returns the file name with extension as a string.

## Example

```pascal
f := FileByIndex(0);
sFileName := GetFileName(f);
AddMessage(sFileName);  // --> 'Skyrim.esm'
```

## See Also

- [FileByIndex](Global_FileByIndex.md)
- [FileByName](Global_FileByName.md)
- [GetFile](IwbElement_GetFile.md)


