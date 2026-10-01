# LocalizationGetStringsFromFile

## Syntax

```pascal
procedure LocalizationGetStringsFromFile(AFileName: string; AStrings: TStrings);
```

## Description

Copies the strings from a localization file the handler has already loaded. `AFileName` is the file name only, compared without regard to case, such as `Skyrim_English.STRINGS`. A path does not match. The call replaces the contents of `AStrings`. It does not append, and it does not open a file from disk.

Each entry's text is the string. The entry's object is the string ID. If that file is not loaded, the list is left unchanged. If the localization handler is not assigned, the call does nothing.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | File name of a localization file the handler has already loaded |
| AStrings | TStrings | List replaced with that file's strings |

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

- [ResourceExists](IwbResource_ResourceExists.md)
