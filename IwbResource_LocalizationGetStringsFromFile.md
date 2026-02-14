# LocalizationGetStringsFromFile

## Syntax

```pascal
procedure LocalizationGetStringsFromFile(aFileName: string; aStrings: TStrings);
```

## Description

Extracts all localized strings from a localization file (.STRINGS, .DLSTRINGS, or .ILSTRINGS) and adds them to a string list. This function uses the localization handler to parse the binary string files used by Skyrim and later games.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | The name of the localization file to read (without path) |
| aStrings | TStrings | The string list to receive the extracted strings |

## Returns

This function does not return a value.

## Example

```pascal
var
  strings: TStringList;
begin
  strings := TStringList.Create;
  try
    LocalizationGetStringsFromFile('Skyrim_English.STRINGS', strings);
    AddMessage('Loaded ' + IntToStr(strings.Count) + ' strings');
  finally
    strings.Free;
  end;
end;
```

## See Also

- [ResourceExists](IwbContainer_ResourceExists.md)
