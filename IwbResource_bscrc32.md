# bscrc32

## Syntax

```pascal
function bscrc32(AString: string): Cardinal;
```

## Description

Calculates a BSCRC32 checksum of the string as written. Letter case and slashes are left alone. This is not the Oblivion or Skyrim BSA filename hash, and it is not a checksum of a file on disk. Fallout 4 archive names go through [CreateHashFO4](IwbResource_CreateHashFO4.md), which lowercases the path and converts slashes first.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AString | string | The string to calculate the CRC32 hash for |

## Returns

Returns a Cardinal value representing the Bethesda-specific CRC32 hash of the input string.

## Example

```pascal
var
  fileName: string;
  hash: Cardinal;
begin
  fileName := 'meshes\armor\iron\ironarmor.nif';
  hash := bscrc32(fileName);
  AddMessage('BSCRC32 for ' + fileName + ': ' + IntToHex(hash, 8));
end;
```

## See Also

- [CreateHashFO4](IwbResource_CreateHashFO4.md)
- [wbCRC32Data](IwbResource_wbCRC32Data.md)
- [wbCRC32File](IwbResource_wbCRC32File.md)
