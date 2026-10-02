# GetIsESM

## Syntax

```pascal
function GetIsESM(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` has the ESM flag set in its header.

This is the master flag, not the file extension. A `.esp` can return `True`. Returns `False` when `AFile` is not a file or is not a plugin.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check |

## Returns

`True` when the ESM flag is set, `False` otherwise.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and GetIsESM(f) then
    AddMessage(GetFileName(f) + ' has the ESM flag');
end;
```

## See Also

- [SetIsESM](IwbFile_SetIsESM.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [GetIsMedium](IwbFile_GetIsMedium.md)
