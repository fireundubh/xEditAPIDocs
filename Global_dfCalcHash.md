# dfCalcHash

## Syntax

```pascal
function dfCalcHash(const Value: string): Cardinal;
```

## Description

Calculates a hash value for a given string, typically used for identifying data format elements or binary data.

This hash function is used internally by xEdit's data format system for quickly identifying and comparing binary structures, particularly in NIF files and other binary formats where string identifiers need to be efficiently looked up or compared. The hash algorithm is consistent across xEdit versions to ensure compatibility when reading and writing binary file formats.

This is particularly useful when working with NIF block types, material property names, or other binary format identifiers that need fast lookup or comparison.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Value | string | The string value to hash |

## Returns

Returns a Cardinal (unsigned 32-bit integer) representing the hash value.

## Example

```pascal
var
  blockName: string;
  hashValue: Cardinal;
begin
  blockName := 'NiNode';
  hashValue := dfCalcHash(blockName);
  AddMessage(Format('Hash of "%s": %u', [blockName, hashValue]));

  // Use for quick comparison
  if dfCalcHash('NiTriShape') = hashValue then
    AddMessage('Block types match');
end;
```

## See Also

- [NifBlockList](IwbResource_NifBlockList.md)
- [wbCRC32Data](IwbResource_wbCRC32Data.md)
