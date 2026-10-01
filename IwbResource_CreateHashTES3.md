# CreateHashTES3

## Syntax

```pascal
function CreateHashTES3(AFileName: string): UInt64;
```

## Description

Creates a Morrowind (TES3)-specific hash value for a given filename. This hash function is used by Morrowind's BSA archive format for file identification and resource lookups.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The filename to calculate the hash for |

## Returns

Returns the hash as a `UInt64`.

## Example

```pascal
var
  resourceName: string;
  hash: UInt64;
begin
  resourceName := 'meshes\i\in_c_stair_plain_tall.nif';
  hash := CreateHashTES3(resourceName);
  AddMessage('TES3 hash: ' + IntToHex64(hash, 16));
end;
```

## See Also

- [CreateHashTES4](IwbResource_CreateHashTES4.md)
- [CreateHashFO4](IwbResource_CreateHashFO4.md)
