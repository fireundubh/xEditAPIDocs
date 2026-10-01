# wbSHA1Data

## Syntax

```pascal
function wbSHA1Data(AData: TBytes): string;
```

## Description

`wbSHA1Data` is not registered. The adapter procedure and its `AddFunction` line are commented out, so a script that calls this name fails as an unknown identifier. Use [wbCRC32Data](IwbResource_wbCRC32Data.md) for a checksum of a byte array.

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
  data := ResourceOpenData('', 'meshes\architecture\whiterun\wrbuildings.nif');
  checksum := wbCRC32Data(data);
  AddMessage(IntToHex(checksum, 8));
end;
```

## See Also

- [wbCRC32Data](IwbResource_wbCRC32Data.md)
- [wbSHA1File](IwbResource_wbSHA1File.md)
- [wbMD5Data](IwbResource_wbMD5Data.md)
