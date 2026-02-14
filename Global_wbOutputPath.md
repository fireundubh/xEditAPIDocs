# wbOutputPath

## Syntax

```pascal
function wbOutputPath: string;
```

## Description

Returns the path to the output directory where xEdit saves generated files. This is typically used for LOD generation, exports, and other file creation operations.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the output directory.

## Example

```pascal
var
  outputDir: string;
  exportFile: string;
begin
  outputDir := wbOutputPath;
  exportFile := outputDir + 'LOD\Meshes\terrain.nif';

  AddMessage('Output directory: ' + outputDir);
  ForceDirectories(ExtractFilePath(exportFile));
end;
```

## See Also

- [wbTempPath](Global_wbTempPath.md)
- [wbDataPath](Global_wbDataPath.md)
