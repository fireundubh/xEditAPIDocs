# CanBeSmall

## Syntax

```pascal
function CanBeSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be a Small file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it can be Small |

## Returns

Returns `True` if the file can be Small, `False` otherwise.

## Example

```pascal
if CanBeSmall(f) then
  SetIsSmall(f, True);
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
