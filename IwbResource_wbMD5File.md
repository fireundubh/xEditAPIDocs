# wbMD5File

## Syntax

```pascal
function wbMD5File(AFileName: string): string;
```

## Description

`wbMD5File` is not registered. The adapter procedure and its `AddFunction` line are commented out, so a script that calls this name fails as an unknown identifier. Use [wbCRC32File](IwbResource_wbCRC32File.md) for a checksum of a file on disk.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | Not available. The commented adapter would have hashed this path |

## Returns

Not available. The commented adapter would have returned a hexadecimal string.

## Example

```pascal
var
  pluginPath: string;
  checksum: Cardinal;
begin
  pluginPath := DataPath + 'MyMod.esp';
  if FileExists(pluginPath) then begin
    checksum := wbCRC32File(pluginPath);
    AddMessage(IntToHex(checksum, 8));
  end;
end;
```

## See Also

- [wbCRC32File](IwbResource_wbCRC32File.md)
- [wbMD5Data](IwbResource_wbMD5Data.md)
- [wbSHA1File](IwbResource_wbSHA1File.md)
