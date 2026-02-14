# wbGameName

## Syntax

```pascal
function wbGameName: string;
```

## Description

Returns the human-readable name of the current game. This is the display name used in the user interface.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the current game's display name (e.g., 'Skyrim', 'Fallout 4', 'Starfield').

## Example

```pascal
var
  gameName: string;
begin
  gameName := wbGameName;
  AddMessage('Current game: ' + gameName);

  if gameName = 'Skyrim Special Edition' then
    AddMessage('Processing SSE data');
end;
```

## See Also

- [wbGameName2](Global_wbGameName2.md)
- [wbGameMode](Global_wbGameMode.md)
- [wbGameMasterEsm](Global_wbGameMasterEsm.md)
