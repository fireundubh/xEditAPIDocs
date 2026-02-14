# wbSettingsFileName

## Syntax

```pascal
function wbSettingsFileName: string;
```

## Description

Returns the full path and filename of the xEdit settings INI file. This file stores all user preferences and configuration options.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the settings INI file.

## Example

```pascal
var
  settingsFile: string;
begin
  settingsFile := wbSettingsFileName;
  AddMessage('Settings file location: ' + settingsFile);

  if FileExists(settingsFile) then
    AddMessage('Settings file exists');
end;
```

## See Also

- [wbSettings](Global_wbSettings.md)
