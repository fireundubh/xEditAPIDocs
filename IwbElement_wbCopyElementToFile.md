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
var
    copiedElement: IwbElement;
begin
    copiedElement := wbCopyElementToFile(sourceElement, targetFile, True, True);
end;
```

## See Also

- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)


