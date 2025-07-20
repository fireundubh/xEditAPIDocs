# SetIsESL

## Syntax

```pascal
procedure SetIsESL(AFile: IwbFile; AIsESL: Boolean);
```

## Description

Sets the ESL flag in `AFile` if `AIsESL` is `True`; otherwise, **SetIsESL** clears the flag.

## Example

```pascal
f := FileByName('MyMod.esl');
SetIsESL(f, True);
```

## See Also

- [GetIsESL - IwbFile](IwbFile_GetIsESL.md)
- [GetIsESM - IwbFile](IwbFile_GetIsESM.md)
- [SetIsESM - IwbFile](IwbFile_SetIsESM.md)
