# wbCopyElementToFileWithPrefixAndSuffix

## Syntax

```pascal
function wbCopyElementToFileWithPrefixAndSuffix(AElement: IwbElement; AFile: IwbFile; AAsNew: Boolean; AAsDeep: Boolean; APrefix: String; ASuffix: String; AReplace: String; AWith: String): IwbElement;
```

## Description

Copies `AElement` to `AFile` with a specified `APrefix` and `ASuffix`. You can also specify a string `AReplace` to be replaced `AWith` in the name.

## Example

```pascal
var
  newElement: IwbElement;
begin
  newElement := wbCopyElementToFileWithPrefixAndSuffix(e, f, True, True, 'Prefix_', '_Suffix', 'Old', 'New');
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
- [wbCopyElementToFileWithPrefix](IwbElement_wbCopyElementToFileWithPrefix.md)
