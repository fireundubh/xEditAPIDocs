# SetIsESL

## Syntax

```pascal
procedure SetIsESL(AFile: IwbFile; AIsESL: Boolean);
```

## Description

Sets or clears the light flag on `AFile`.

[SetIsLight](IwbFile_SetIsLight.md) and [SetIsSmall](IwbFile_SetIsSmall.md) write the same flag. This does not move the file into a light load-order slot. [CanBeESL](IwbFile_CanBeESL.md) only reports the current slot.

Nothing changes when the game has no light plugins, or when `AFile` is not a plugin. Changing the flag on a file that is not editable raises.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to change |
| AIsESL | Boolean | `True` sets the light flag, `False` clears it |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('MyMod.esp');
  if Assigned(f) then
    SetIsESL(f, True);
end;
```

## See Also

- [GetIsESL](IwbFile_GetIsESL.md)
- [SetIsLight](IwbFile_SetIsLight.md)
- [SetIsESM](IwbFile_SetIsESM.md)
