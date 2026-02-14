# GetIsSmall

## Syntax

```pascal
function GetIsSmall(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is a Small file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it is Small |

## Returns

Returns `True` if the file is Small, `False` otherwise.

## Example

```pascal
if GetIsSmall(f) then
  AddMessage(GetFileName(f) + ' is small');
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [SetIsSmall](IwbFile_SetIsSmall.md)
