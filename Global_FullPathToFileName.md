# FullPathToFileName

## Syntax

```pascal
function FullPathToFileName(AFileName: string): string;
```

## Description

Resolves the full filesystem path for a given filename.

Returns the complete path to the specified file, including drive letter and all directory components.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The filename to resolve to a full path |

## Returns

Returns the complete filesystem path as a string.

## Example

```pascal
var
  fullPath: string;
begin
  fullPath := FullPathToFileName('Skyrim.esm');
  AddMessage('Full path: ' + fullPath);
end;
```

## See Also

- [FileByName](Global_FileByName.md)


