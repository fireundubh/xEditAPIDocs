# TempPath

## Syntax

```pascal
function TempPath: string;
```

## Description

Returns the path to the temporary files directory used by xEdit. This directory is used for storing temporary data during processing operations.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the temporary directory.

## Example

```pascal
var
  tempDir: string;
  tempFile: string;
begin
  tempDir := TempPath;
  tempFile := tempDir + 'processing_cache.tmp';

  // Use temp file for intermediate processing
  AddMessage('Using temp directory: ' + tempDir);
end;
```

## See Also

- [wbTempPath](Global_wbTempPath.md)
- [ProgramPath](Global_ProgramPath.md)
