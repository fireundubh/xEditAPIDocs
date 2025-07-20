# SetIsESM

## Syntax

```pascal
procedure SetIsESM(AFile: IwbFile; AIsESM: Boolean);
```

## Description

Sets the ESM flag in `AFile` if `AIsESM` is `True`; otherwise, **SetIsESM** clears the flag.

## Example

```pascal
f := FileByName('MyMod.esm');
SetIsESM(f, True);
```

## See Also

- [GetIsESL - IwbFile](IwbFile_GetIsESL.md)
- [GetIsESM - IwbFile](IwbFile_GetIsESM.md)
- [SetIsESL - IwbFile](IwbFile_SetIsESL.md)
