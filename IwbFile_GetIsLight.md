# GetIsLight

## Syntax

```pascal
function GetIsLight(AFile: IwbFile): Boolean;
```

## Description

Checks whether the file has the Light (ESL) flag set.

This function retrieves the IsLight property, which checks the file header flag indicating light plugin status. Light plugins use a special FormID range (FE xxx) and don't consume a full load order slot. Returns false for invalid files. Light status affects FormID assignment and load order counting. Use CanBeLight to check if a file is eligible to be flagged as light.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it is Light |

## Returns

Returns `True` if the file is Light, `False` otherwise.

## Example

```pascal
if GetIsLight(f) then
  AddMessage(GetFileName(f) + ' is light');
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
- [GetIsESL](IwbFile_GetIsESL.md)
