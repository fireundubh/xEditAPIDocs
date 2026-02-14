# wbSHA1File

## Syntax

```pascal
function wbSHA1File(aFileName: string): string;
```

## Description

Calculates a SHA-1 hash for a file on disk and returns it as a hexadecimal string. This function reads the entire file and computes its SHA-1 hash for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | The full path to the file to calculate the SHA-1 hash for |

## Returns

Returns a string containing the hexadecimal SHA-1 hash of the file.

## Example

```pascal
var
  pluginPath: string;
  hash: string;
begin
  pluginPath := DataPath + 'MyMod.esp';

  if FileExists(pluginPath) then begin
    hash := wbSHA1File(pluginPath);
    AddMessage('Plugin SHA-1: ' + hash);
  end;
end;
```

## See Also

- [wbSHA1Data](IwbResource_wbSHA1Data.md)
- [wbMD5File](IwbResource_wbMD5File.md)
- [wbCRC32File](IwbResource_wbCRC32File.md)
