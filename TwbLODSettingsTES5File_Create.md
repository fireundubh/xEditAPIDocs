# TwbLODSettingsTES5File.Create

## Syntax

```pascal
function TwbLODSettingsTES5File.Create: TwbLODSettingsTES5File;
```

## Description

Creates a new LOD settings file handler for Skyrim, Skyrim Special Edition, and Fallout 4.

xEdit loads these as `lodsettings\<Worldspace>.lod`. The file stores `Min X`, `Min Y`, `Stride`, `Min Level`, and `Max Level`. Those are cell bounds and LOD level indexes, not fade distances. The Fallout 3 settings file is a different, larger record.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading and modifying those fields.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODSettingsTES5File` instance ready for loading or creating a Skyrim or Fallout 4 LOD settings file.

## Example

```pascal
var
  lodSettings: TwbLODSettingsTES5File;
begin
  lodSettings := TwbLODSettingsTES5File.Create;
  try
    lodSettings.LoadFromFile('lodsettings\Tamriel.lod');

    AddMessage('Min level: ' + lodSettings.EditValues['Min Level']);
    AddMessage('Max level: ' + lodSettings.EditValues['Max Level']);
    AddMessage('Stride: ' + lodSettings.EditValues['Stride']);

    lodSettings.EditValues['Max Level'] := '32';
    lodSettings.SaveToFile('lodsettings\Tamriel_edit.lod');
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
