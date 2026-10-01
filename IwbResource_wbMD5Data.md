# wbMD5Data

## Syntax

```pascal
function wbMD5Data(AData: TBytes): string;
```

## Description

`wbMD5Data` is not registered. The adapter procedure and its `AddFunction` line are commented out, so a script that calls this name fails as an unknown identifier. Use [wbCRC32Data](IwbResource_wbCRC32Data.md) for a checksum of a byte array.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | Not available. The commented adapter would have hashed these bytes |

## Returns

Not available. The commented adapter would have returned a hexadecimal string.

## Example

```pascal
var
  data: TBytes;
  checksum: Cardinal;
begin
  data := ResourceOpenData('', 'meshes\armor\iron\ironarmor.nif');
  checksum := wbCRC32Data(data);
  AddMessage(IntToHex(checksum, 8));
end;
```

## See Also

- [wbCRC32Data](IwbResource_wbCRC32Data.md)
- [wbMD5File](IwbResource_wbMD5File.md)
- [wbSHA1Data](IwbResource_wbSHA1Data.md)
