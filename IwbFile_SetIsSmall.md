# SetIsSmall

## Syntax

```pascal
procedure SetIsSmall(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets or clears the light flag on `AFile`.

There is no separate small-plugin flag. [SetIsLight](IwbFile_SetIsLight.md) and [SetIsESL](IwbFile_SetIsESL.md) write the same flag. [CanBeSmall](IwbFile_CanBeSmall.md) only reports whether the current load-order slot is a light slot.

Nothing changes when the game has no light plugins, or when `AFile` is not a plugin. Changing the flag on a file that is not editable raises.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to change |
| AValue | Boolean | `True` sets the light flag, `False` clears it |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('MyMod.esp');
  if Assigned(f) then
    SetIsSmall(f, True);
end;
```

## See Also

- [CanBeSmall](IwbFile_CanBeSmall.md)
- [GetIsSmall](IwbFile_GetIsSmall.md)
- [SetIsLight](IwbFile_SetIsLight.md)
