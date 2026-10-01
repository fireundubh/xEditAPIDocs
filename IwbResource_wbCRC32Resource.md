# wbCRC32Resource

## Syntax

```pascal
function wbCRC32Resource(AContainerName: string; AResourceName: string): Cardinal;
```

## Description

Reads a resource with [ResourceOpenData](IwbResource_ResourceOpenData.md) and returns [wbCRC32Data](IwbResource_wbCRC32Data.md) of those bytes. An empty `AContainerName` uses the last loaded container that has the file. A missing file is hashed as empty data, which is 0. It does not raise.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | Container name, or `''` for the last loaded match |
| AResourceName | string | The path to the resource within the archive |

## Returns

Returns a Cardinal value representing the CRC32 checksum of the resource data.

## Example

```pascal
var
  checksum: Cardinal;
begin
  checksum := wbCRC32Resource('', 'meshes\architecture\whiterun\wrbuildings.nif');
  AddMessage('Resource CRC32: ' + IntToHex(checksum, 8));
end;
```

## See Also

- [wbCRC32Data](IwbResource_wbCRC32Data.md)
- [wbCRC32File](IwbResource_wbCRC32File.md)
- [ResourceOpenData](IwbResource_ResourceOpenData.md)
