# CreateHashFO4

## Syntax

```pascal
function CreateHashFO4(AFileName: string): Cardinal;
```

## Description

Calculates the BA2 filename hash used by Fallout 4. The path is lowercased and `/` is turned into `\` before the hash. Letter case and slash style in the argument do not change the result. [bscrc32](IwbResource_bscrc32.md) hashes the string as written and does not do that.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | The filename to calculate the hash for |

## Returns

Returns the hash as a `Cardinal`.

## Example

```pascal
var
  resourceName: string;
  hash: Cardinal;
begin
  resourceName := 'textures\landscape\grass01.dds';
  hash := CreateHashFO4(resourceName);
  AddMessage('FO4 hash: ' + IntToHex(hash, 8));
end;
```

## See Also

- [CreateHashTES4](IwbResource_CreateHashTES4.md)
- [CreateHashTES3](IwbResource_CreateHashTES3.md)
