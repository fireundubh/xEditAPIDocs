# TwbLODSettingsTES5File.Create

## Syntax

```pascal
function TwbLODSettingsTES5File.Create: TwbLODSettingsTES5File;
```

## Description

Creates a new LOD Settings file handler for Skyrim/Fallout 4 format.

LOD Settings files control the Level of Detail rendering system parameters for Skyrim, Skyrim Special Edition, and Fallout 4. They define distance thresholds, fade ranges, quality levels, and other parameters that control LOD object and terrain rendering. These settings balance visual quality against performance by controlling when simplified geometry replaces full-detail models.

The format is more advanced than the Fallout 3 version, with additional settings for object LOD, tree LOD, and terrain LOD subsystems.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading and modifying LOD generation parameters.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODSettingsTES5File` instance ready for loading or creating Skyrim/Fallout 4 LOD settings data.

## Example

```pascal
var
  lodSettings: TwbLODSettingsTES5File;
begin
  lodSettings := TwbLODSettingsTES5File.Create;
  try
    // Load LOD settings for Skyrim worldspace
    lodSettings.LoadFromFile('Meshes\Terrain\Tamriel\TamrielLODSettings.lod');

    // Read object LOD settings
    AddMessage('Object LOD4: ' + lodSettings.ElementByName('Object LOD Level 4', True).EditValue);
    AddMessage('Tree LOD4: ' + lodSettings.ElementByName('Tree LOD Level 4', True).EditValue);

    // Adjust for ultra quality
    lodSettings.ElementByName('Object LOD Level 4', True).EditValue := '16384';
    lodSettings.SaveToFile('Meshes\Terrain\Tamriel\TamrielLODSettings_Ultra.lod');
  finally
    lodSettings.Free;
  end;
end;
```

## See Also

- [TwbLODSettingsFO3File.Create](TwbLODSettingsFO3File_Create.md) - Fallout 3 LOD settings format
- [GenerateLODTES5Objects](Global_GenerateLODTES5Objects.md)
- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
