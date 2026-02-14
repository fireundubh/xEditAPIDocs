# GetIsESM

## Syntax

```pascal
function GetIsESM(AFile: IwbFile): Boolean;
```

## Description

Checks whether the file has the ESM (Elder Scrolls Master) flag set.

This function retrieves the IsESM property, which checks the file header flag indicating master file status. ESM files load before ESP files and can be referenced by other plugins. Returns false for invalid files. Note: This checks the flag in the file header, not the file extension. A .esp file can have the ESM flag set and vice versa.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it's an ESM |

## Returns

Returns true if the file is an ESM plugin, false otherwise.

## Example

```pascal
if GetIsESM(f) then
  AddMessage(GetFileName(f) + ' is an ESM!');
```

## See Also

- [SetIsESM](IwbFile_SetIsESM.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [GetIsMedium](IwbFile_GetIsMedium.md)
- [CanBeLight](IwbFile_CanBeLight.md)

