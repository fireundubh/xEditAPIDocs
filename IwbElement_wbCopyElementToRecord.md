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
var
  copiedElement: IwbElement;
begin
  copiedElement := wbCopyElementToRecord(sourceElement, targetRecord, True, True);
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)


