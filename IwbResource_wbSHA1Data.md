# wbSHA1Data

## Syntax

```pascal
function wbSHA1Data(aData: TBytes): string;
```

## Description

Calculates a SHA-1 hash for the provided binary data and returns it as a hexadecimal string. SHA-1 is a cryptographic hash function commonly used for data integrity verification.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aData | TBytes | The binary data to calculate the SHA-1 hash for |

## Returns

Returns a string containing the hexadecimal SHA-1 hash of the input data.

## Example

```pascal
var
  resourceData: TBytes;
  hash: string;
begin
  resourceData := ResourceOpenData('', 'meshes\architecture\whiterun\wrbuildings.nif');
  hash := wbSHA1Data(resourceData);

  AddMessage('SHA-1 hash: ' + hash);
end;
```

## See Also

- [wbSHA1File](IwbResource_wbSHA1File.md)
- [wbMD5Data](IwbResource_wbMD5Data.md)
- [wbCRC32Data](IwbResource_wbCRC32Data.md)
