# wbCopyElementToFile

## Syntax

```pascal
function wbCopyElementToFile(AElement: IwbElement; AFile: IwbFile; AAsNew: boolean; ADeepCopy: boolean): IwbElement;
```

## Description

Copies an element to another file.

Parameters:

- `AElement`: Source element (IwbMainRecord, IwbGroupRecord, or IwbContainer)
- `AFile`: Destination file
- `AAsNew`: When true, creates new record instead of override
- `ADeepCopy`: When true, performs deep copy of the element

Returns the copied element.

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


