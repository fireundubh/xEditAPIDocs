# wbCopyElementToFileWithPrefixAndSuffix

## Syntax

```pascal
function wbCopyElementToFileWithPrefixAndSuffix(AElement: IwbElement; AFile: IwbFile; AAsNew: Boolean; AAsDeep: Boolean; APrefix: String; ASuffix: String; AReplace: String; AWith: String): IwbElement;
```

## Description

Copies `AElement` to `AFile` with a specified `APrefix` and `ASuffix`. You can also specify a string `AReplace` to be replaced `AWith` in the name.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to copy |
| AFile | IwbFile | The destination file to copy to |
| AAsNew | Boolean | Whether to create a new record with a new Form ID |
| AAsDeep | Boolean | Whether to perform a deep copy |
| APrefix | String | The prefix to add to the element name |
| ASuffix | String | The suffix to add to the element name |
| AReplace | String | The string to replace in the element name |
| AWith | String | The replacement string |

## Returns

Returns the copied IwbElement.

## Example

```pascal
// Example 1: Copy with prefix, suffix, and string replacement
var
  targetFile: IwbFile;
  newRec: IwbMainRecord;
  newEdid: string;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(FileCount - 1);
    if Assigned(targetFile) then begin
      // Add 'Custom' prefix, '_V2' suffix, replace 'Iron' with 'Steel'
      newRec := wbCopyElementToFileWithPrefixAndSuffix(e, targetFile,
        True, True, 'Custom', '_V2', 'Iron', 'Steel');
      if Assigned(newRec) then begin
        newEdid := EditorID(newRec);
        AddMessage(Format('Created: %s -> %s', [EditorID(e), newEdid]));
        // 'IronSword' becomes 'CustomSteelSword_V2'
      end;
    end;
  end;
end;

// Example 2: Batch copy with naming transformation
var
  sourceRec: IwbMainRecord;
  targetFile: IwbFile;
  copiedRec: IwbMainRecord;
  i: integer;
  copyCount: integer;
begin
  targetFile := FileByIndex(FileCount - 1);
  if Assigned(targetFile) then begin
    copyCount := 0;
    for i := 0 to RecordCount - 1 do begin
      sourceRec := RecordByIndex(i);
      if Assigned(sourceRec) and (Signature(sourceRec) = 'ARMO') then begin
        // Convert 'DLC' to 'Mod', add 'Enhanced' prefix
        copiedRec := wbCopyElementToFileWithPrefixAndSuffix(sourceRec, targetFile,
          True, True, 'Enhanced', '', 'DLC', 'Mod');
        if Assigned(copiedRec) then
          Inc(copyCount);
      end;
    end;
    AddMessage(Format('Copied %d armor records', [copyCount]));
  end;
end;

// Example 3: Version update with systematic renaming
var
  targetFile: IwbFile;
  updatedRec: IwbMainRecord;
  sourceEdid: string;
begin
  if Assigned(e) then begin
    sourceEdid := EditorID(e);
    targetFile := FileByLoadOrder(255);
    if Assigned(targetFile) then begin
      // Update version in name: v1 -> v2, add 'Updated' suffix
      updatedRec := wbCopyElementToFileWithPrefixAndSuffix(e, targetFile,
        True, True, '', '_Updated', 'v1', 'v2');
      if Assigned(updatedRec) then
        AddMessage(Format('Updated: %s -> %s',
          [sourceEdid, EditorID(updatedRec)]));
    end;
  end;
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)
