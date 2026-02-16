# ConvertBlock

## Syntax

```pascal
procedure ConvertBlock(Index: Integer; ABlockType: string);
```

Access via: `nifFile.ConvertBlock(Index, BlockType)`

## Description

Converts a block at the specified index to a different block type. This attempts to preserve compatible data fields while changing the block's type.

This is useful for:
- Converting between similar block types (e.g., NiTriShape to BSTriShape)
- Upgrading blocks to newer versions
- Changing node types while preserving children and properties

The conversion preserves fields that exist in both the source and destination block types. Fields that don't exist in the destination type are lost, and new fields in the destination type are initialized to defaults.

After conversion, all references to this block remain valid because the block index doesn't change. However, you should verify that the conversion preserved the data you need.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | The index of the block to convert |
| ABlockType | string | The new block type |

## Returns

This is a procedure (no return value). The block at the specified index is modified in place.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\solitude\sroofcorner01.nif');

    // Find and convert all NiTriShape blocks to BSTriShape
    for i := nif.BlocksCount - 1 downto 0 do begin
      block := nif.Blocks[i];

      if block.BlockType = 'NiTriShape' then begin
        AddMessage('Converting block ' + IntToStr(i) + ' to BSTriShape');
        nif.ConvertBlock(i, 'BSTriShape');
      end;
    end;

    nif.SaveToFile('meshes\architecture\solitude\sroofcorner01_converted.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_CopyBlock](TwbNifFile_CopyBlock.md)
- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
- [TwbNifBlock_BlockType](TwbNifBlock_BlockType.md)
- [TwbNifFile_Blocks](TwbNifFile_Blocks.md)
