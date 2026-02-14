# CanBeLight

## Syntax

```pascal
function CanBeLight(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Light file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it can be Light |

## Returns

Returns `True` if the file can be Light, `False` otherwise.

## Example

```pascal
if CanBeLight(f) then
  SetIsLight(f, True);
```

## See Also

- [CanBeESL](IwbFile_CanBeESL.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsLight](IwbFile_SetIsLight.md)
