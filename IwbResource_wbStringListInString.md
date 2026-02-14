# wbStringListInString

## Syntax

```pascal
function wbStringListInString(aStringList: TStringList; aString: string): Integer;
```

## Description

Searches for the first occurrence of any string from a string list within a target string using case-insensitive comparison. Returns the index of the first matching string found.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aStringList | TStringList | The list of strings to search for |
| aString | string | The target string to search within |

## Returns

Returns the index (0-based) of the first string from the list found within the target string, or -1 if no match is found.

## Example

```pascal
var
  keywords: TStringList;
  description: string;
  foundIndex: Integer;
begin
  keywords := TStringList.Create;
  try
    keywords.Add('sword');
    keywords.Add('armor');
    keywords.Add('potion');

    description := 'This is an iron armor piece';
    foundIndex := wbStringListInString(keywords, description);

    if foundIndex >= 0 then
      AddMessage('Found keyword: ' + keywords[foundIndex]);
  finally
    keywords.Free;
  end;
end;
```

## See Also

- [wbFilterStrings](Global_wbFilterStrings.md)
