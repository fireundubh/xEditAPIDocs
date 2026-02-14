# DataPath

## Syntax

```pascal
function DataPath: string;
```

## Description

Returns the path to the game's Data directory. This is the directory where the game stores all plugin files, meshes, textures, and other resources.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the game's Data directory.

## Example

```pascal
var
  dataDir: string;
  customFile: string;
begin
  dataDir := DataPath;
  customFile := dataDir + 'Meshes\Custom\mymodel.nif';

  if FileExists(customFile) then
    AddMessage('Custom mesh found at: ' + customFile);
end;
```

## See Also

- [wbDataPath](Global_wbDataPath.md)
- [ProgramPath](Global_ProgramPath.md)
- [ScriptsPath](Global_ScriptsPath.md)
