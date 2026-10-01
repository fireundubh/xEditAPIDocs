# wbCRC32File

## Syntax

```pascal
function wbCRC32File(AFileName: string): Cardinal;
```

## Description

Calculates a CRC32 checksum for a file on disk. Returns 0 when the file does not exist. A path that exists but cannot be read raises.

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
