# wbMD5File

## Syntax

```pascal
function wbMD5File(AFileName: string): string;
```

## Description

Calculates an MD5 hash for a file on disk and returns it as a hexadecimal string. This function reads the entire file and computes its MD5 hash for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The full path to the file to calculate the MD5 hash for |

## Returns

Returns a string containing the hexadecimal MD5 hash of the file.

## Example

```pascal
var
  pluginPath: string;
  hash: string;
begin
  pluginPath := DataPath + 'MyMod.esp';

  if FileExists(pluginPath) then begin
    hash := wbMD5File(pluginPath);
    AddMessage('Plugin MD5: ' + hash);
  end;
end;
```

## See Also

- [wbMD5Data](IwbResource_wbMD5Data.md)
- [wbSHA1File](IwbResource_wbSHA1File.md)
- [wbCRC32File](IwbResource_wbCRC32File.md)
