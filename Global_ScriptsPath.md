# ScriptsPath

## Syntax

```pascal
function ScriptsPath: string;
```

## Description

Returns the path to the xEdit scripts directory. This is where user scripts (.pas files) are stored and loaded from when executing automation tasks.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the scripts directory.

## Example

```pascal
var
  scriptsDir: string;
  myScript: string;
begin
  scriptsDir := ScriptsPath;
  myScript := scriptsDir + 'Export\ExportJSON.pas';

  if FileExists(myScript) then
    AddMessage('Export script found');
end;
```

## See Also

- [wbScriptsPath](Global_wbScriptsPath.md)
- [ProgramPath](Global_ProgramPath.md)
- [DataPath](Global_DataPath.md)
