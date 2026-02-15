# BlocksCount

## Syntax

```pascal
function BlocksCount(ANifFile: TwbNifFile): Integer;
```

## Description

Returns the total number of blocks in the NIF file. This includes the header, footer (if present), and all scene graph blocks.

The block count represents all blocks in the file's linear block list. Blocks are indexed from 0 to BlocksCount-1. The first block (index 0) is always the header, and subsequent blocks contain nodes, geometry, properties, and other NIF data.

This count is automatically maintained by the TwbNifFile class when blocks are added, inserted, or removed.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |

## Returns

Returns the total number of blocks as an integer.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\furniture\blacksmith\blacksmithforgemarker.nif');

    AddMessage('NIF contains ' + IntToStr(nif.BlocksCount) + ' blocks');

    // Iterate through all blocks
    for i := 0 to nif.BlocksCount - 1 do begin
      block := nif.Blocks[i];
      AddMessage(Format('Block %d: %s', [i, BlockType(block)]));
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_Blocks](TwbNifFile_Blocks.md)
- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNifFile_Header](TwbNifFile_Header.md)
