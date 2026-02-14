# wbGameMode

## Syntax

```pascal
function wbGameMode: TwbGameMode;
```

## Description

Returns the current game mode enumeration value. This identifies which game xEdit is currently configured for and determines how records are interpreted.

## Parameters

This function takes no parameters.

## Returns

Returns a TwbGameMode enumeration value (gmTES3, gmTES4, gmTES5, gmSSE, gmFO3, gmFNV, gmFO4, gmFO76, gmSF1, etc.).

## Example

```pascal
begin
  case wbGameMode of
    gmTES5, gmSSE: AddMessage('Running in Skyrim mode');
    gmFO4: AddMessage('Running in Fallout 4 mode');
    gmFO76: AddMessage('Running in Fallout 76 mode');
    gmSF1: AddMessage('Running in Starfield mode');
  else
    AddMessage('Running in other game mode');
  end;
end;
```

## See Also

- [wbGameName](Global_wbGameName.md)
- [wbGameMasterEsm](Global_wbGameMasterEsm.md)
