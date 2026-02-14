# FileCount

## Syntax

```pascal
function FileCount: integer;
```

## Description

Returns the length of the array of loaded files in the active session

## Parameters

This function takes no parameters.

## Returns

Returns the number of loaded files as an integer.

## Examples

```pascal
var
  i: integer;
  f: IwbFile;
begin
  AddMessage('xEdit has ' + IntToStr(FileCount) + ' files loaded');
  
  for i := 0 to Pred(FileCount) do
  begin
    f := FileByIndex(i);
    AddMessage(GetFileName(f));
  end;
end;
```

## See Also

- [FileByIndex](Global_FileByIndex.md)
- [FileByName](Global_FileByName.md)
- [GetFileName](IwbFile_GetFileName.md)


