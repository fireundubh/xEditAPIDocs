# SetIsSmall

## Syntax

```pascal
procedure SetIsSmall(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets whether `AFile` is a Small file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to set the Small flag on |
| AValue | Boolean | Whether to set (True) or clear (False) the Small flag |

## Example

```pascal
if CanBeSmall(f) then
  SetIsSmall(f, True);
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
