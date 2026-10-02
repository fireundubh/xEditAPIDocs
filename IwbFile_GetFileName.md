# GetFileName

## Syntax

```pascal
function GetFileName(AElement: IwbElement): string;
```

## Description

Returns the file name of a loaded file.

Pass an `IwbFile` to get that file's name. Pass any other element to get the name of the file that contains it. An element that is not in a file, or a value that is not an element, returns an empty string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | A file, or an element inside a file |

## Returns

The file name, or an empty string when there is no file.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) then
    AddMessage(GetFileName(f));
  if Assigned(e) then
    AddMessage(GetFileName(e));
end;
```

## See Also

- [FileByIndex](Global_FileByIndex.md)
- [FileByName](Global_FileByName.md)
- [GetFile](IwbElement_GetFile.md)
