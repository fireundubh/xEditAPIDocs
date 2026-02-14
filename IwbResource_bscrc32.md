# bscrc32

## Syntax

```pascal
function bscrc32(aString: string): Cardinal;
```

## Description

Calculates a Bethesda-specific CRC32 checksum for a given string. This hash function is used by Bethesda's game engines for file identification and resource lookups in BSA archives.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aString | string | The string to calculate the CRC32 hash for |

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
  AddMessage('BSA hash for ' + fileName + ': ' + IntToHex(hash, 8));
end;
```

## See Also

- [wbCRC32File](IwbResource_wbCRC32File.md)
- [wbCRC32Data](IwbResource_wbCRC32Data.md)
