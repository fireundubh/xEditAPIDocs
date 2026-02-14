# wbSettings

## Syntax

```pascal
function wbSettings: TCustomIniFile;
```

## Description

Returns the settings configuration object used by xEdit. This provides access to all user preferences and configuration options stored in the INI file.

## Parameters

This function takes no parameters.

## Returns

Returns a TCustomIniFile object representing the xEdit settings.

## Example

```pascal
var
  settings: TCustomIniFile;
  windowWidth: Integer;
begin
  settings := wbSettings;

  if Assigned(settings) then begin
    windowWidth := settings.ReadInteger('Window', 'Width', 1024);
    AddMessage('Window width setting: ' + IntToStr(windowWidth));
  end;
end;
```

## See Also

- [wbSettingsFileName](Global_wbSettingsFileName.md)
