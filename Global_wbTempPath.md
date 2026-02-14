# wbTempPath

## Syntax

```pascal
function wbTempPath: string;
```

## Description

Returns the path to the temporary files directory used by xEdit. This directory is used for storing temporary data during processing operations. This is an alias for the TempPath function.

## Parameters

This function takes no parameters.

## Returns

Returns a string containing the full path to the temporary directory.

## Example

```pascal
var
  tempDir: string;
  cacheFile: string;
begin
  tempDir := wbTempPath;
  cacheFile := tempDir + 'export_cache.dat';

  AddMessage('Temp directory: ' + tempDir);
end;
```

## See Also

- [TempPath](Global_TempPath.md)
- [wbOutputPath](Global_wbOutputPath.md)
