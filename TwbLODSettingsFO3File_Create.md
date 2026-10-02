# TwbLODSettingsFO3File.Create

## Syntax

```pascal
function TwbLODSettingsFO3File.Create: TwbLODSettingsFO3File;
```

## Description

Creates a new LOD settings file handler for Fallout 3 and Fallout New Vegas.

xEdit loads these as `lodsettings\<Worldspace>.dlodsettings`. The file stores the terrain LOD level range (`Min Terrain Level`, `Max Terrain Level`), `Stride`, cell bounds (`Min X`, `Min Y`, `Max X`, `Max Y`), and `Object Level`. It does not store per-level fade distances.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading and modifying those fields.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODSettingsFO3File` instance ready for loading or creating a Fallout 3 or New Vegas LOD settings file.

## Example

```pascal
var
  lodSettings: TwbLODSettingsFO3File;
begin
  lodSettings := TwbLODSettingsFO3File.Create;
  try
    lodSettings.LoadFromFile('lodsettings\Wasteland.dlodsettings');

    AddMessage('Min terrain level: ' + lodSettings.EditValues['Min Terrain Level']);
    AddMessage('Max terrain level: ' + lodSettings.EditValues['Max Terrain Level']);
    AddMessage('Object level: ' + lodSettings.EditValues['Object Level']);

    lodSettings.EditValues['Object Level'] := '4';
    lodSettings.SaveToFile('lodsettings\Wasteland_edit.dlodsettings');
  finally
    lodSettings.Free;
  end;
end;
```

## See Also

- [TwbLODSettingsTES5File.Create](TwbLODSettingsTES5File_Create.md) - Skyrim LOD settings format
- [GenerateLODTES4](Global_GenerateLODTES4.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
