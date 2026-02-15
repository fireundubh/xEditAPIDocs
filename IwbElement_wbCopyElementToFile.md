# wbCopyElementToFile

## Syntax

```pascal
function wbCopyElementToFile(AElement: IwbElement; AFile: IwbFile; AAsNew: boolean; ADeepCopy: boolean): IwbElement;
```

## Description

Copies an element to another file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The source element to copy (IwbMainRecord, IwbGroupRecord, or IwbContainer) |
| AFile | IwbFile | The destination file |
| AAsNew | boolean | When true, creates new record instead of override |
| ADeepCopy | boolean | When true, performs deep copy of the element |

## Returns

Returns the copied element as an IwbElement interface.

## Example

```pascal
// Example 1: Create override in target plugin
var
  targetFile: IwbFile;
  overrideRec: IwbElement;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(FileCount - 1);
    if Assigned(targetFile) then begin
      // AsNew=False creates override, DeepCopy=True copies all data
      overrideRec := wbCopyElementToFile(e, targetFile, False, True);
      if Assigned(overrideRec) then
        AddMessage(Format('Created override of %s in %s',
          [EditorID(e), GetFileName(targetFile)]));
    end;
  end;
end;

// Example 2: Copy as new record with new FormID
var
  targetFile: IwbFile;
  newRec: IwbMainRecord;
  edidElement: IwbElement;
begin
  if Assigned(e) then begin
    targetFile := FileByLoadOrder(255);
    if Assigned(targetFile) then begin
      // AsNew=True creates new record with new FormID
      newRec := wbCopyElementToFile(e, targetFile, True, True);
      if Assigned(newRec) then begin
        edidElement := ElementByPath(newRec, 'EDID');
        if Assigned(edidElement) then
          SetEditValue(edidElement, EditorID(e) + '_Copy');
        AddMessage(Format('Created new record %s [%s]',
          [EditorID(newRec), IntToHex(FormID(newRec), 8)]));
      end;
    end;
  end;
end;

// Example 3: Shallow vs deep copy comparison
var
  targetFile: IwbFile;
  shallowCopy, deepCopy: IwbElement;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(FileCount - 1);
    if Assigned(targetFile) then begin
      // Shallow copy (DeepCopy=False) - references only
      shallowCopy := wbCopyElementToFile(e, targetFile, True, False);
      if Assigned(shallowCopy) then
        AddMessage('Shallow copy created (references preserved)');

      // Deep copy (DeepCopy=True) - all data duplicated
      deepCopy := wbCopyElementToFile(e, targetFile, True, True);
      if Assigned(deepCopy) then
        AddMessage('Deep copy created (all data duplicated)');
    end;
  end;
end;
```

## See Also

- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)


