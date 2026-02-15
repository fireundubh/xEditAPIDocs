# wbCopyElementToRecord

## Syntax

```pascal
function wbCopyElementToRecord(AElement: IwbElement; ARecord: IwbMainRecord; AAsNew: boolean; ADeepCopy: boolean): IwbElement;
```

## Description

Copies an element to another record.

Useful for copying specific elements like "Conditions" or faction entries between records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The source element to copy |
| ARecord | IwbMainRecord | The destination record |
| AAsNew | boolean | When true, creates new record instead of override |
| ADeepCopy | boolean | When true, performs deep copy |

## Returns

Returns the copied element as an IwbElement interface.

## Example

```pascal
// Example 1: Copy conditions from one record to another
var
  targetRec: IwbMainRecord;
  conditions: IwbElement;
  copiedConditions: IwbElement;
begin
  targetRec := RecordByFormID(FileByIndex(0), $00012345, True);
  if Assigned(e) and Assigned(targetRec) then begin
    conditions := ElementByPath(e, 'Conditions');
    if Assigned(conditions) then begin
      copiedConditions := wbCopyElementToRecord(conditions, targetRec, False, True);
      if Assigned(copiedConditions) then
        AddMessage(Format('Copied conditions to %s', [EditorID(targetRec)]));
    end;
  end;
end;

// Example 2: Copy keywords array
var
  targetRec: IwbMainRecord;
  sourceKwda: IwbElement;
  copiedKwda: IwbElement;
begin
  targetRec := RecordByEditorID('TargetRecord');
  if Assigned(e) and Assigned(targetRec) then begin
    sourceKwda := ElementByPath(e, 'KWDA');
    if Assigned(sourceKwda) then begin
      copiedKwda := wbCopyElementToRecord(sourceKwda, targetRec, False, True);
      if Assigned(copiedKwda) then
        AddMessage(Format('Copied %d keywords to %s',
          [ElementCount(copiedKwda), EditorID(targetRec)]));
    end;
  end;
end;

// Example 3: Copy model data between records
var
  targetRec: IwbMainRecord;
  modelData: IwbElement;
  copiedModel: IwbElement;
begin
  targetRec := RecordByFormID(FileByIndex(0), $00067890, True);
  if Assigned(e) and Assigned(targetRec) then begin
    modelData := ElementByPath(e, 'Model');
    if Assigned(modelData) then begin
      // Remove existing model in target
      RemoveElement(targetRec, 'Model');

      // Copy model from source
      copiedModel := wbCopyElementToRecord(modelData, targetRec, False, True);
      if Assigned(copiedModel) then
        AddMessage(Format('Copied model data to %s', [EditorID(targetRec)]));
    end;
  end;
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)


