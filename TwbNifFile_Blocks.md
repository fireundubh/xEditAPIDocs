# Blocks

## Syntax

```pascal
property Blocks[Index: Integer]: TwbNifBlock;
```

Access via: `nifFile.Blocks[Index]`

## Description

Returns a specific block from the NIF file by its index in the block list. Blocks are indexed from 0 to BlocksCount-1.

This indexed property provides direct access to any block in the file's linear block list. Block 0 is always the header. The order of blocks matters in NIF files because blocks reference each other by index.

Use this when you know the specific block index you need, or when iterating through all blocks. For finding blocks by type or other criteria, use the BlockByType or BlocksByType methods instead.

This is a read-only indexed property.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index of the block to retrieve |

## Returns

Returns the TwbNifBlock at the specified index.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
  blockName: string;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\common\platter01.nif');

    // Access blocks by index
    for i := 0 to nif.BlocksCount - 1 do begin
      block := nif.Blocks[i];

      // Get block type
      AddMessage(Format('Block[%d]: Type = %s', [i, block.BlockType]));

      // Try to get name if it's a named block
      if block.StringsCount > 0 then begin
        blockName := block.Strings[0].EditValue;
        if blockName <> '' then
          AddMessage('  Name: ' + blockName);
      end;
    end;

    // Access specific block
    block := nif.Blocks[1]; // Get second block
    AddMessage('Second block type: ' + block.BlockType);
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNifFile_BlocksByType](TwbNifFile_BlocksByType.md)
- [TwbNifBlock_BlockType](TwbNifBlock_BlockType.md)
