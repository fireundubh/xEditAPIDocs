# wbCopyElementToRecord

## Syntax

```pascal
function wbCopyElementToRecord(AElement: IwbElement; ARecord: IwbMainRecord; AAsNew: boolean; ADeepCopy: boolean): IwbElement;
```

## Description

Copies an element to another record.

Useful for copying specific elements like "Conditions" or faction entries between records.

Parameters:

- `AElement`: Source element to copy
- `ARecord`: Destination record
- `AAsNew`: When true, creates new record instead of override
- `ADeepCopy`: When true, performs deep copy

Returns the copied element.

## Example

```pascal
var
  copiedElement: IwbElement;
begin
  copiedElement := wbCopyElementToRecord(sourceElement, targetRecord, True, True);
end;
```

## See Also

- [wbCopyElementToFile - IwbElement](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToFileWithPrefix - IwbElement](IwbElement_wbCopyElementToFileWithPrefix.md)
