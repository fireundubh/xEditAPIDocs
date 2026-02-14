# GetFileName

## Syntax

```pascal
function GetFileName(AFile: IwbFile): String;
```

## Description

Returns the plugin filename with extension (e.g., "Skyrim.esm", "MyMod.esp").

This function retrieves the FileName property from either an IwbFile or IwbElement interface. For IwbFile, it returns the file's own name. For IwbElement, it traverses to the containing file and returns that file's name. Returns an empty string for invalid inputs. The filename does not include the directory path, only the base name and extension.

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


