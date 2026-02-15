# GetFile

## Syntax

```pascal
function GetFile(AElement: IwbElement): IwbFile;
```

## Description

Returns the plugin file that contains this element.

This function retrieves the _File property, which provides access to the IwbFile interface representing the plugin (esp/esm/esl) that owns this element. All elements within a file hierarchy return the same file reference. Returns nil if the element is invalid or detached from a file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the containing file for |

## Returns

Returns the containing file as an IwbFile interface.

## Example

```pascal
// Example 1: Get plugin name from element
var
  element: IwbElement;
  pluginFile: IwbFile;
  fileName: string;
begin
  if Assigned(e) then begin
    element := ElementByPath(e, 'EDID');
    if Assigned(element) then begin
      pluginFile := GetFile(element);
      if Assigned(pluginFile) then begin
        fileName := GetFileName(pluginFile);
        AddMessage(Format('Element is in plugin: %s', [fileName]));
      end;
    end;
  end;
end;

// Example 2: Check if records are in same file
var
  rec2: IwbMainRecord;
  file1, file2: IwbFile;
  fileName1, fileName2: string;
begin
  rec2 := WinningOverride(e);
  if Assigned(e) and Assigned(rec2) then begin
    file1 := GetFile(e);
    file2 := GetFile(rec2);
    if Assigned(file1) and Assigned(file2) then begin
      fileName1 := GetFileName(file1);
      fileName2 := GetFileName(file2);
      if file1 = file2 then
        AddMessage(Format('Both records in same file: %s', [fileName1]))
      else
        AddMessage(Format('Master: %s | Override: %s', [fileName1, fileName2]));
    end;
  end;
end;

// Example 3: Cross-reference element locations
var
  baseElement: IwbElement;
  baseRecord: IwbMainRecord;
  sourceFile, targetFile: IwbFile;
  sourceName, targetName: string;
begin
  if Assigned(e) then begin
    baseElement := ElementByPath(e, 'NAME');
    if Assigned(baseElement) then begin
      baseRecord := LinksTo(baseElement);
      if Assigned(baseRecord) then begin
        sourceFile := GetFile(e);
        targetFile := GetFile(baseRecord);
        if Assigned(sourceFile) and Assigned(targetFile) then begin
          sourceName := GetFileName(sourceFile);
          targetName := GetFileName(targetFile);
          AddMessage(Format('%s [%s] -> %s [%s]',
            [EditorID(e), sourceName, EditorID(baseRecord), targetName]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [ContainingMainRecord](IwbElement_ContainingMainRecord.md)
- [GetContainer](IwbElement_GetContainer.md)
- [GetFileName](IwbFile_GetFileName.md)


