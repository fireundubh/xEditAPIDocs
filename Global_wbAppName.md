# wbAppName

## Syntax

```pascal
function wbAppName: string;
```

## Description

Returns the name of the current xEdit application variant. This will be different depending on which tool is running (e.g., 'TES5Edit', 'SSEEdit', 'FO4Edit', etc.).

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the application name.

## Example

```pascal
var
  appName: string;
begin
  appName := wbAppName;
  AddMessage('Running application: ' + appName);

  if appName = 'SSEEdit' then
    AddMessage('This is Skyrim Special Edition');
end;
```

## See Also

- [wbGameName](Global_wbGameName.md)
- [wbGameMode](Global_wbGameMode.md)
