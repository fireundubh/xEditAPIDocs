# wbProgramPath

## Syntax

```pascal
function wbProgramPath: string;
```

## Description

Returns the path to the xEdit executable's directory. This is the directory where the xEdit program is located, useful for accessing configuration files or other program resources. This is an alias for the ProgramPath function.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the xEdit program directory.

## Example

```pascal
var
  programDir: string;
  iniFile: string;
begin
  programDir := wbProgramPath;
  iniFile := programDir + 'SSEEdit.ini';

  AddMessage('Program directory: ' + programDir);
end;
```

## See Also

- [ProgramPath](Global_ProgramPath.md)
- [wbScriptsPath](Global_wbScriptsPath.md)
- [wbDataPath](Global_wbDataPath.md)
