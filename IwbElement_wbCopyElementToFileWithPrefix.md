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
var
    copiedElement: IwbElement;
begin
    copiedElement := wbCopyElementToFileWithPrefix(sourceElement, targetFile, True, True, 'Old', 'New', '_Copy');
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToRecord](IwbElement_wbCopyElementToRecord.md)


