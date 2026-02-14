# ProgramPath

## Syntax

```pascal
function ProgramPath: string;
```

## Description

Returns the path to the xEdit executable's directory. This is the directory where the xEdit program is located, useful for accessing configuration files or other program resources.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the xEdit program directory.

## Example

```pascal
var
  programDir: string;
  configFile: string;
begin
  programDir := ProgramPath;
  configFile := programDir + 'Settings.ini';

  if FileExists(configFile) then
    AddMessage('Settings file found at: ' + configFile);
end;
```

## See Also

- [wbProgramPath](Global_wbProgramPath.md)
- [DataPath](Global_DataPath.md)
- [ScriptsPath](Global_ScriptsPath.md)
