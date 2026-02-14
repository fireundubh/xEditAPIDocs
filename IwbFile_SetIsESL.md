# SetIsESL

## Syntax

```pascal
procedure SetIsESL(AFile: IwbFile; AIsESL: Boolean);
```

## Description

Sets the ESL flag in `AFile` if `AIsESL` is `True`; otherwise, **SetIsESL** clears the flag.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to set the ESL flag on |
| AIsESL | Boolean | Whether to set (True) or clear (False) the ESL flag |

## Example

```pascal
f := FileByName('MyMod.esl');
SetIsESL(f, True);
```

## See Also

- [GetIsESL](IwbFile_GetIsESL.md)
- [GetIsESM](IwbFile_GetIsESM.md)
- [SetIsESM](IwbFile_SetIsESM.md)


