# FileCount

## Syntax

```pascal
function FileCount: integer;
```

## Description

Returns the length of the array of loaded files in the active session

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

- [FileByIndex - Global](Global_FileByIndex.md)
- [FileByName - Global](Global_FileByName.md)
- [GetFileName - IwbFile](IwbFile_GetFileName.md)
