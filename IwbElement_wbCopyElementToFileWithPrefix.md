# wbCopyElementToFileWithPrefix

## Syntax

```pascal
function wbCopyElementToFileWithPrefix(ASource: IwbElement; AFile: IwbFile; AAsNew: boolean; ADeepCopy: boolean; APrefixRemove: string; APrefix: string; ASuffix: string): IwbElement;
```

## Description

Copies an element to another file with prefix/suffix manipulation.

Parameters:

- `ASource`: Source element to copy
- `AFile`: Destination file
- `AAsNew`: When true, creates new record instead of override
- `ADeepCopy`: When true, performs deep copy
- `APrefixRemove`: Prefix to remove from names
- `APrefix`: Prefix to add to names
- `ASuffix`: Suffix to add to names

Returns the copied element.

## Example

```pascal
var
    copiedElement: IwbElement;
begin
    copiedElement := wbCopyElementToFileWithPrefix(sourceElement, targetFile, True, True, 'Old', 'New', '_Copy');
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md)


