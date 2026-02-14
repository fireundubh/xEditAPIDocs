# wbDataPath

## Syntax

```pascal
function wbDataPath: string;
```

## Description

Returns the path to the game's Data directory. This is the directory where the game stores all plugin files, meshes, textures, and other resources. This is an alias for the DataPath function.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the game's Data directory.

## Example

```pascal
var
  dataDir: string;
  meshPath: string;
begin
  dataDir := wbDataPath;
  meshPath := dataDir + 'Meshes\';

  AddMessage('Game data directory: ' + dataDir);
end;
```

## See Also

- [DataPath](Global_DataPath.md)
- [wbProgramPath](Global_wbProgramPath.md)
- [wbScriptsPath](Global_wbScriptsPath.md)
