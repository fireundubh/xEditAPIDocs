# SetIsLight

## Syntax

```pascal
procedure SetIsLight(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets or clears the light flag in `AFile`'s header.

[SetIsESL](IwbFile_SetIsESL.md) and [SetIsSmall](IwbFile_SetIsSmall.md) write the same flag. This does not move the file into a light load-order slot. [CanBeLight](IwbFile_CanBeLight.md) only reports the current slot, so it is not a test of whether the flag may be set.

Nothing changes when the game has no light plugins, or when `AFile` is not a plugin. Changing the flag on a file that is not editable raises. The change is in memory until the file is saved. New FormIDs allocated after the flag is set use the light object-id range.

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
    SetIsLight(f, True);
end;
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsLight](IwbFile_GetIsLight.md)
- [SetIsESL](IwbFile_SetIsESL.md)
