# wbScriptsPath

## Syntax

```pascal
function wbScriptsPath: string;
```

## Description

Returns the path to the xEdit scripts directory. This is where user scripts (.pas files) are stored and loaded from when executing automation tasks. This is an alias for the ScriptsPath function.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the scripts directory.

## Example

```pascal
var
  scriptsDir: string;
  libPath: string;
begin
  scriptsDir := wbScriptsPath;
  libPath := scriptsDir + 'lib\';

  AddMessage('Scripts directory: ' + scriptsDir);
end;
```

## See Also

- [ScriptsPath](Global_ScriptsPath.md)
- [wbProgramPath](Global_wbProgramPath.md)
