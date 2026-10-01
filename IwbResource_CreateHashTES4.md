# CreateHashTES4

## Syntax

```pascal
function CreateHashTES4(AFileName: string): UInt64;
function CreateHashTES4(AFileName: string; AHasExtension: Boolean): UInt64;
```

## Description

Calculates the BSA filename hash used by Oblivion, Fallout 3, Fallout New Vegas, and Skyrim. The path is lowercased before hashing.

The one-argument call passes `AHasExtension` as False. False hashes the whole string as the name and does not treat a trailing extension as an extension, so the `.nif`, `.dds`, `.kf`, and `.wav` bits are not set. True splits on the last `.`, hashes the name and the extension separately, and sets those bits. True with no `.` in the name behaves like False. The second argument is a Boolean, not an extension string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | Filename to hash |
| AHasExtension | Boolean | Optional. True splits off the extension and hashes it. False, and the one-argument call, do not |

## Returns

Returns the hash as a `UInt64`.

## Example

```pascal
var
  resourceName: string;
  hash: UInt64;
begin
  resourceName := 'textures\effects\fxfluidstream.dds';
  hash := CreateHashTES4(resourceName, True);
  AddMessage('TES4 hash: ' + IntToHex64(hash, 16));

  hash := CreateHashTES4(resourceName, False);
  AddMessage('TES4 hash without extension split: ' + IntToHex64(hash, 16));
end;
```

## See Also

- [CreateHashTES3](IwbResource_CreateHashTES3.md)
- [CreateHashFO4](IwbResource_CreateHashFO4.md)
