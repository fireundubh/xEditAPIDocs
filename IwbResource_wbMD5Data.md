# wbMD5Data

## Syntax

```pascal
function wbMD5Data(aData: TBytes): string;
```

## Description

Calculates an MD5 hash for the provided binary data and returns it as a hexadecimal string. MD5 is a cryptographic hash function commonly used for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aData | TBytes | The binary data to calculate the MD5 hash for |

## Returns

Returns a string containing the hexadecimal MD5 hash of the input data.

## Example

```pascal
var
  fileData: TBytes;
  hash: string;
begin
  fileData := ResourceOpenData('', 'meshes\armor\iron\ironarmor.nif');
  hash := wbMD5Data(fileData);

  AddMessage('MD5 hash: ' + hash);
end;
```

## See Also

- [wbMD5File](IwbResource_wbMD5File.md)
- [wbSHA1Data](IwbResource_wbSHA1Data.md)
- [wbCRC32Data](IwbResource_wbCRC32Data.md)
