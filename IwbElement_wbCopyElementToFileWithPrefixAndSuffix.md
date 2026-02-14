# wbCopyElementToFileWithPrefixAndSuffix

## Syntax

```pascal
function wbCopyElementToFileWithPrefixAndSuffix(AElement: IwbElement; AFile: IwbFile; AAsNew: Boolean; AAsDeep: Boolean; APrefix: String; ASuffix: String; AReplace: String; AWith: String): IwbElement;
```

## Description

Copies `AElement` to `AFile` with a specified `APrefix` and `ASuffix`. You can also specify a string `AReplace` to be replaced `AWith` in the name.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to copy |
| AFile | IwbFile | The destination file to copy to |
| AAsNew | Boolean | Whether to create a new record with a new Form ID |
| AAsDeep | Boolean | Whether to perform a deep copy |
| APrefix | String | The prefix to add to the element name |
| ASuffix | String | The suffix to add to the element name |
| AReplace | String | The string to replace in the element name |
| AWith | String | The replacement string |

## Returns

Returns the copied IwbElement.

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
