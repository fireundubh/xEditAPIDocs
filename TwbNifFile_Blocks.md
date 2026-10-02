# Blocks

## Syntax

```pascal
property Blocks[Index: Integer]: TwbNifBlock;
```

Access via: `nifFile.Blocks[Index]`

## Description

Returns a specific block from the NIF file by its index in the block list. Blocks are indexed from 0 to BlocksCount-1.

This indexed property provides direct access to a block in the file. Index 0 is the first block after the header, not the header itself. `BlocksCount` does not include the header or the footer; use [Header](TwbNifFile_Header.md) and [Footer](TwbNifFile_Footer.md) for those. The order of blocks matters because blocks reference each other by index.

Use this when you know the specific block index you need, or when iterating through all blocks. For finding blocks by type or other criteria, use the BlockByType or BlocksByType methods instead.

This is a read-only indexed property.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | Zero-based index into the block list, excluding the header and footer. Valid range is 0 to BlocksCount-1 |

## Returns

Returns the TwbNifBlock at the specified index. An index outside that range raises an exception.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
  nameElement: TdfElement;
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
        nameElement := block.Strings[0];
        if Assigned(nameElement) then begin
          blockName := nameElement.EditValue;
          if blockName <> '' then
            AddMessage('  Name: ' + blockName);
        end;
      end;
    end;

    if nif.BlocksCount > 1 then begin
      block := nif.Blocks[1];
      AddMessage('Second block type: ' + block.BlockType);
    end;
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
