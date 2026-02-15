# BaseName

## Syntax

```pascal
function BaseName(AElement: IwbElement): string;
```

## Description

Returns the element's name without load order prefixes or other decorations.

This function retrieves the BaseName property, which provides the undecorated element identifier. For files, this returns just the filename without the load order index prefix (e.g., "Plugin.esp" instead of "[02] Plugin.esp"). For other elements, behavior is similar to Name. Useful when you need the clean identifier for comparisons or when building user-facing strings. Returns an empty string for invalid elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element whose base name to retrieve |

## Returns

Returns the base name of the element as a string, without load order prefixes for file elements.

## Example

```pascal
// Example 1: Get clean file name without load order prefix
var
  rec: IwbMainRecord;
  pluginFile: IwbFile;
  baseName, displayName: string;
begin
  if Assigned(e) then begin
    pluginFile := GetFile(rec);
    if Assigned(pluginFile) then begin
      baseName := BaseName(pluginFile);
      displayName := Name(pluginFile);
      AddMessage('Base name: ' + baseName);
      AddMessage('Display name: ' + displayName);
      // Base: "MyMod.esp", Display: "[05] MyMod.esp"
    end;
  end;
end;

// Example 2: Compare base names for file matching
var
  rec: IwbMainRecord;
  masterFile, currentFile: IwbFile;
  masterBase, currentBase: string;
begin
  if Assigned(e) then begin
    currentFile := GetFile(rec);
    masterFile := MasterOrSelf(rec)._File;
    if Assigned(currentFile) and Assigned(masterFile) then begin
      currentBase := BaseName(currentFile);
      masterBase := BaseName(masterFile);
      if currentBase = masterBase then
        AddMessage('Record is in master file: ' + masterBase)
      else
        AddMessage(Format('Override from %s to %s', [masterBase, currentBase]));
    end;
  end;
end;

// Example 3: Build file list without load order prefixes
var
  i: integer;
  pluginFile: IwbFile;
  baseName: string;
  fileList: TStringList;
begin
  fileList := TStringList.Create;
  try
    for i := 0 to FileCount - 1 do begin
      pluginFile := FileByIndex(i);
      if Assigned(pluginFile) then begin
        baseName := BaseName(pluginFile);
        fileList.Add(baseName);
      end;
    end;
    fileList.Sort;
    AddMessage('Loaded plugins (alphabetical):');
    for i := 0 to fileList.Count - 1 do
      AddMessage('  ' + fileList[i]);
  finally
    fileList.Free;
  end;
end;
```

## See Also

- [Name](IwbElement_Name.md)
- [DisplayName](IwbElement_DisplayName.md)
- [ShortName](IwbElement_ShortName.md)


