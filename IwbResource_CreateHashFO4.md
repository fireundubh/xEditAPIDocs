# CreateHashFO4

## Syntax

```pascal
function CreateHashFO4(aFileName: string): UInt64;
```

## Description

Creates a Fallout 4-specific hash value for a given filename. This hash function is used by Fallout 4's BA2 archive format for file identification and resource lookups.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | The filename to calculate the hash for |

## Returns

Returns a UInt64 value representing the Fallout 4-specific hash of the filename.

## Example

```pascal
var
  resourceName: string;
  hash: UInt64;
begin
  resourceName := 'textures\landscape\grass01.dds';
  hash := CreateHashFO4(resourceName);
  AddMessage('FO4 hash: ' + IntToHex(hash, 16));
end;
```

## See Also

- [CreateHashTES4](IwbResource_CreateHashTES4.md)
- [CreateHashTES3](IwbResource_CreateHashTES3.md)
