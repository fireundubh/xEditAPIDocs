# SetIsESM

## Syntax

```pascal
procedure SetIsESM(AFile: IwbFile; AIsESM: Boolean);
```

## Description

Sets or clears the ESM flag in `AFile`'s header.

This is the master flag, not the file extension. Nothing changes when `AFile` is not a plugin. Changing the flag on a file that is not editable raises. The change is in memory until the file is saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to change |
| AIsESM | Boolean | `True` sets the ESM flag, `False` clears it |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('MyMod.esp');
  if Assigned(f) then
    SetIsESM(f, True);
end;
```

## See Also

- [GetIsESM](IwbFile_GetIsESM.md)
- [SetIsESL](IwbFile_SetIsESL.md)
- [SetIsLight](IwbFile_SetIsLight.md)
