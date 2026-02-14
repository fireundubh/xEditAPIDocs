# CreateHashTES4

## Syntax

```pascal
function CreateHashTES4(AFileName: string): UInt64;
function CreateHashTES4(AFileName: string; AExt: string): UInt64;
```

## Description

Creates a TES4-specific hash value for a given filename. This hash function is used by Oblivion, Fallout 3, Fallout New Vegas, and Skyrim's BSA archive formats for file identification and resource lookups. The function can optionally accept a separate extension parameter.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The filename to calculate the hash for |
| AExt | string | Optional. The file extension to use separately in hash calculation |

## Returns

Returns a UInt64 value representing the TES4-specific hash of the filename.

## Example

```pascal
var
  resourceName: string;
  hash: UInt64;
begin
  resourceName := 'textures\effects\fxfluidstream.dds';
  hash := CreateHashTES4(resourceName);
  AddMessage('TES4 hash: ' + IntToHex(hash, 16));

  // Alternative with separate extension
  hash := CreateHashTES4('textures\effects\fxfluidstream', 'dds');
end;
```

## See Also

- [CreateHashTES3](IwbResource_CreateHashTES3.md)
- [CreateHashFO4](IwbResource_CreateHashFO4.md)
