# wbSelectedFilesToFileNames

## Syntax

```pascal
procedure wbSelectedFilesToFileNames(aFileNames: TStrings);
```

## Description

Retrieves the filenames of all currently selected files and main records in the navigation tree view. For main records, their containing file's name is added to the list. Duplicate filenames are automatically prevented.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileNames | TStrings | The string list to receive the unique filenames |

## Returns

This function does not return a value.

## Example

```pascal
var
  selectedFiles: TStringList;
  i: Integer;
begin
  selectedFiles := TStringList.Create;
  try
    wbSelectedFilesToFileNames(selectedFiles);

    AddMessage('Selected files:');
    for i := 0 to selectedFiles.Count - 1 do
      AddMessage('  ' + selectedFiles[i]);
  finally
    selectedFiles.Free;
  end;
end;
```

## See Also

- [FileByName](Global_FileByName.md)
