# FullPathToFileName

## Syntax

```pascal
function FullPathToFileName(AFileName: string): string;
```

## Description

Resolves the full filesystem path for a given filename.

Returns the complete path to the specified file, including drive letter and all directory components.

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

- [FileByName - Global](Global_FileByName.md)
