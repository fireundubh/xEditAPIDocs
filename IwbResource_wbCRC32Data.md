# wbCRC32Data

## Syntax

```pascal
function wbCRC32Data(AData: TBytes): Cardinal;
```

## Description

Calculates a standard CRC32 checksum for the provided binary data. This is a general-purpose checksum function used for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The binary data to calculate the CRC32 checksum for |

## Returns

Returns a Cardinal value representing the CRC32 checksum of the input data.

## Example

```pascal
var
  fileData: TBytes;
  checksum: Cardinal;
begin
  fileData := ResourceOpenData('', 'meshes\clutter\book01.nif');
  checksum := wbCRC32Data(fileData);

  AddMessage('CRC32 checksum: ' + IntToHex(checksum, 8));
end;
```

## See Also

- [wbCRC32File](IwbResource_wbCRC32File.md)
- [wbCRC32Resource](IwbResource_wbCRC32Resource.md)
- [wbMD5Data](IwbResource_wbMD5Data.md)
