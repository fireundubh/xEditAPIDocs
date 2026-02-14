# FileByLoadOrderFileID

## Syntax

```pascal
function FileByLoadOrderFileID(ALoadOrderFileID: string): IwbFile;
```

## Description

Retrieves a file by its load order file ID string. The load order file ID is the hexadecimal prefix used in FormIDs to identify which plugin a record belongs to.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ALoadOrderFileID | string | The load order file ID as a hexadecimal string (e.g., 'FE000ABC' or '05') |

## Returns

Returns an IwbFile interface for the file with the matching load order file ID, or nil if not found.

## Example

```pascal
var
  modFile: IwbFile;
begin
  // Get the file with load order file ID '05'
  modFile := FileByLoadOrderFileID('05');

  if Assigned(modFile) then
    AddMessage('File found: ' + modFile.FileName);
end;
```

## See Also

- [FileByLoadOrder](Global_FileByLoadOrder.md)
- [FileByName](Global_FileByName.md)
- [FileByIndex](Global_FileByIndex.md)
