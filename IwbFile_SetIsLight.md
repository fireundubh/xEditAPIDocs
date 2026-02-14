# SetIsLight

## Syntax

```pascal
procedure SetIsLight(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Light file.

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
