# wbCRC32File

## Syntax

```pascal
function wbCRC32File(AFileName: string): Cardinal;
```

## Description

Calculates a standard CRC32 checksum for a file on disk. This function reads the entire file and computes its checksum for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The full path to the file to calculate the CRC32 checksum for |

## Returns

Returns a Cardinal value representing the CRC32 checksum of the file.

## Example

```pascal
var
  pluginPath: string;
  checksum: Cardinal;
begin
  pluginPath := DataPath + 'MyMod.esp';

  if FileExists(pluginPath) then begin
    checksum := wbCRC32File(pluginPath);
    AddMessage('Plugin CRC32: ' + IntToHex(checksum, 8));
  end;
end;
```

## See Also

- [wbCRC32Data](IwbResource_wbCRC32Data.md)
- [wbCRC32Resource](IwbResource_wbCRC32Resource.md)
- [wbMD5File](IwbResource_wbMD5File.md)
