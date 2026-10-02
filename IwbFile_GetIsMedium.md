# GetIsMedium

## Syntax

```pascal
function GetIsMedium(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` is medium.

In pseudo-medium mode this is the pseudo-medium state. Otherwise, when the game supports medium plugins and `AFile` is a plugin, this is the header medium flag. Otherwise it is `False`. It is not the load-order slot. [CanBeMedium](IwbFile_CanBeMedium.md) tests the slot.

Returns `False` when `AFile` is not a file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check |

## Returns

`True` when the check above matches, `False` when it does not or when `AFile` is not a file.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and GetIsMedium(f) then
    AddMessage(GetFileName(f) + ' is medium');
end;
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [SetIsMedium](IwbFile_SetIsMedium.md)
