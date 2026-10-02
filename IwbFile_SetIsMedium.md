# SetIsMedium

## Syntax

```pascal
procedure SetIsMedium(AFile: IwbFile; AValue: Boolean);
```

## Description

Sets or clears the medium flag in `AFile`'s header.

This does not move the file into a medium load-order slot. [CanBeMedium](IwbFile_CanBeMedium.md) only reports the current slot.

Nothing changes when the game has no medium plugins, or when `AFile` is not a plugin. Changing the flag on a file that is not editable raises. The change is in memory until the file is saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to change |
| AValue | Boolean | `True` sets the medium flag, `False` clears it |

## Returns

Returns nothing.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByName('MyMod.esp');
  if Assigned(f) then
    SetIsMedium(f, True);
end;
```

## See Also

- [CanBeMedium](IwbFile_CanBeMedium.md)
- [GetIsMedium](IwbFile_GetIsMedium.md)
