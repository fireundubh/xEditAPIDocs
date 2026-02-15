# TwbLODSettingsFO3File.Create

## Syntax

```pascal
function TwbLODSettingsFO3File.Create: TwbLODSettingsFO3File;
```

## Description

Creates a new LOD Settings file handler for Fallout 3/New Vegas format.

LOD Settings files control the Level of Detail rendering system parameters for Fallout 3 and Fallout New Vegas. They define distance thresholds, fade settings, quality levels, and other parameters that control when and how LOD objects are rendered. These settings optimize performance by showing simplified geometry at greater distances.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading and modifying LOD generation parameters.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODSettingsFO3File` instance ready for loading or creating Fallout 3/New Vegas LOD settings data.

## Example

```pascal
var
  lodSettings: TwbLODSettingsFO3File;
begin
  lodSettings := TwbLODSettingsFO3File.Create;
  try
    // Load LOD settings for a worldspace
    lodSettings.LoadFromFile('Meshes\Landscape\LOD\Wasteland\WastelandLODSettings.lod');

    // Read LOD distance settings
    AddMessage('LOD4 distance: ' + lodSettings.ElementByName('LOD4 Distance', True).EditValue);
    AddMessage('LOD8 distance: ' + lodSettings.ElementByName('LOD8 Distance', True).EditValue);

    // Modify settings for better quality
    lodSettings.ElementByName('LOD4 Distance', True).EditValue := '8192';
    lodSettings.SaveToFile('Meshes\Landscape\LOD\Wasteland\WastelandLODSettings_HQ.lod');
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
