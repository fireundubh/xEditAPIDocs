# wbCopyElementToFileWithPrefix

## Syntax

```pascal
function wbCopyElementToFileWithPrefix(ASource: IwbElement; AFile: IwbFile; AAsNew: boolean; ADeepCopy: boolean; APrefixRemove: string; APrefix: string; ASuffix: string): IwbElement;
```

## Description

Copies an element to another file with prefix/suffix manipulation.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ASource | IwbElement | The source element to copy |
| AFile | IwbFile | The destination file |
| AAsNew | boolean | When true, creates new record instead of override |
| ADeepCopy | boolean | When true, performs deep copy |
| APrefixRemove | string | Prefix to remove from names |
| APrefix | string | Prefix to add to names |
| ASuffix | string | Suffix to add to names |

## Returns

Returns the copied element as an IwbElement interface.

## Example

```pascal
// Example 1: Copy record with prefix modification
var
  targetFile: IwbFile;
  newRec: IwbMainRecord;
  newEdid: string;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(FileCount - 1);
    if Assigned(targetFile) then begin
      // Remove 'AAA' prefix, add 'BBB' prefix, add '_New' suffix
      newRec := wbCopyElementToFileWithPrefix(e, targetFile, True, True,
        'AAA', 'BBB', '_New');
      if Assigned(newRec) then begin
        newEdid := EditorID(newRec);
        AddMessage(Format('Created %s from %s', [newEdid, EditorID(e)]));
        // If source was 'AAAWeaponSword', result is 'BBBWeaponSword_New'
      end;
    end;
  end;
end;

// Example 2: Batch copy with naming convention
var
  sourceRec: IwbMainRecord;
  targetFile: IwbFile;
  copiedRec: IwbMainRecord;
  i: integer;
begin
  targetFile := FileByIndex(FileCount - 1);
  if Assigned(targetFile) then begin
    for i := 0 to RecordCount - 1 do begin
      sourceRec := RecordByIndex(i);
      if Assigned(sourceRec) and (Signature(sourceRec) = 'WEAP') then begin
        // Add 'Custom' prefix to all weapons
        copiedRec := wbCopyElementToFileWithPrefix(sourceRec, targetFile, True, True,
          '', 'Custom', '');
        if Assigned(copiedRec) then
          AddMessage(Format('Copied: %s -> %s',
            [EditorID(sourceRec), EditorID(copiedRec)]));
      end;
    end;
  end;
end;

// Example 3: Replace prefix for mod compatibility
var
  targetFile: IwbFile;
  compatRec: IwbMainRecord;
  oldPrefix, newPrefix: string;
begin
  if Assigned(e) then begin
    targetFile := FileByLoadOrder(255);
    oldPrefix := 'DLC01';
    newPrefix := 'MyMod';

    if Assigned(targetFile) then begin
      // Replace DLC01 prefix with MyMod prefix
      compatRec := wbCopyElementToFileWithPrefix(e, targetFile, True, True,
        oldPrefix, newPrefix, '');
      if Assigned(compatRec) then
        AddMessage(Format('Compatibility copy: %s -> %s',
          [EditorID(e), EditorID(compatRec)]));
    end;
  end;
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md)


