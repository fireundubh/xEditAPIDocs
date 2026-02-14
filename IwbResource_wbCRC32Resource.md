# wbCRC32Resource

## Syntax

```pascal
function wbCRC32Resource(aContainerName: string; aResourceName: string): Cardinal;
```

## Description

Calculates a standard CRC32 checksum for a resource file stored in a BSA or BA2 archive. This function opens the resource from the archive and computes its checksum.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aContainerName | string | The name of the BSA/BA2 archive containing the resource (empty string searches all) |
| aResourceName | string | The path to the resource within the archive |

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
- [ResourceOpenData](IwbContainer_ResourceOpenData.md)
