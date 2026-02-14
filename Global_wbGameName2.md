# wbGameName2

## Syntax

```pascal
function wbGameName2: string;
```

## Description

Returns an alternative or abbreviated name for the current game. This may differ from wbGameName and is used for specific identification purposes.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing an alternative name for the current game.

## Example

```pascal
var
  gameName2: string;
begin
  gameName2 := wbGameName2;
  AddMessage('Game alternate name: ' + gameName2);
end;
```

## See Also

- [wbGameName](Global_wbGameName.md)
- [wbGameMode](Global_wbGameMode.md)
