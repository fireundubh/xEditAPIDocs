# CreateHashTES3

## Syntax

```pascal
function CreateHashTES3(aFileName: string): Cardinal;
```

## Description

Creates a Morrowind (TES3)-specific hash value for a given filename. This hash function is used by Morrowind's BSA archive format for file identification and resource lookups.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aFileName | string | The filename to calculate the hash for |

## Returns

Returns a Cardinal value representing the TES3-specific hash of the filename.

## Example

```pascal
var
  resourceName: string;
  hash: Cardinal;
begin
  resourceName := 'meshes\i\in_c_stair_plain_tall.nif';
  hash := CreateHashTES3(resourceName);
  AddMessage('TES3 hash: ' + IntToHex(hash, 8));
end;
```

## See Also

- [CreateHashTES4](IwbResource_CreateHashTES4.md)
- [CreateHashFO4](IwbResource_CreateHashFO4.md)
