# BlocksCount

## Syntax

```pascal
property BlocksCount: Integer;
```

Access via: `nifFile.BlocksCount`

## Description

Returns the number of blocks in the NIF file, excluding the header and the footer. Blocks are indexed from 0 to BlocksCount-1. Index 0 is the first scene block, not the header.

This count is automatically maintained by the TwbNifFile class when blocks are added, inserted, or removed.

This is a read-only property.

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
      AddMessage(Format('Block %d: %s', [i, block.BlockType]));
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
