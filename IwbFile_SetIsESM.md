# SetIsESM

## Syntax

```pascal
procedure SetIsESM(AFile: IwbFile; AIsESM: Boolean);
```

## Description

Sets the ESM flag in `AFile` if `AIsESM` is `True`; otherwise, **SetIsESM** clears the flag.

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


