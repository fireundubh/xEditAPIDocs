# wbGameMasterEsm

## Syntax

```pascal
function wbGameMasterEsm: string;
```

## Description

Returns the filename of the master ESM file for the current game. This is the main plugin file that all other plugins depend on (e.g., 'Skyrim.esm', 'Fallout4.esm', 'Oblivion.esm').

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the master ESM filename for the current game.

## Example

```pascal
var
  masterFile: string;
begin
  masterFile := wbGameMasterEsm;
  AddMessage('Game master file: ' + masterFile);

  if masterFile = 'Skyrim.esm' then
    AddMessage('This is Skyrim');
end;
```

## See Also

- [wbGameName](Global_wbGameName.md)
- [wbGameMode](Global_wbGameMode.md)
