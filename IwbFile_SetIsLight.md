# SetIsLight

## Syntax

```pascal
procedure SetIsLight(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets or clears the Light (ESL) flag in the file header.

This function assigns to the IsLight property, which modifies the file header flag controlling light plugin status. Setting this to true marks the file as light, enabling the special FE FormID range and allowing it to not consume a full load order slot. Check CanBeLight before setting to ensure the file is eligible. The change takes effect immediately in memory but must be saved to persist.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to set the Light flag on |
| AValue | Boolean | Whether to set (True) or clear (False) the Light flag |

## Example

```pascal
if CanBeLight(f) then
  SetIsLight(f, True);
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsESL](IwbFile_SetIsESL.md)
