# SetIsESM

## Syntax

```pascal
procedure SetIsESM(AFile: IwbFile; AIsESM: Boolean);
```

## Description

Sets or clears the ESM (Elder Scrolls Master) flag in the file header.

This function assigns to the IsESM property, which modifies the file header flag controlling master file status. Setting this to true marks the file as a master, which affects load order priority and allows other plugins to depend on it. The change takes effect immediately in memory but must be saved to persist. Changing this flag may affect load order on next game launch.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to set the ESM flag on |
| AIsESM | Boolean | Whether to set (True) or clear (False) the ESM flag |

## Example

```pascal
f := FileByName('MyMod.esm');
SetIsESM(f, True);
```

## See Also

- [GetIsESL](IwbFile_GetIsESL.md)
- [GetIsESM](IwbFile_GetIsESM.md)
- [SetIsESL](IwbFile_SetIsESL.md)


