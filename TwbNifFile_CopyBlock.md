# CopyBlock

## Syntax

```pascal
function CopyBlock(Index: Integer): TwbNifBlock;
```

Access via: `nifFile.CopyBlock(Index)`

## Description

Creates a complete copy of the block at the specified index and adds the copy to the end of the NIF file's block list. Returns the newly created copy.

This creates a deep copy of the block, duplicating all of its data. The copy is a separate block with its own index and can be modified independently of the original.

Note that this copies the block's data but does not automatically duplicate any blocks that the original block references. If you need to duplicate an entire branch of the scene graph (a block and all its children), you would need to recursively copy the referenced blocks as well.

After copying, you may need to update references to integrate the copied block into the scene graph.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Index | Integer | The index of the block to copy |

## Returns

Returns the newly created copy of the block.

## Example

```pascal
var
  nif: TwbNifFile;
  original: TwbNifBlock;
  copy: TwbNifBlock;
  origIndex: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\pottery\pot01.nif');

    // Find a block to copy
    original := nif.BlockByType('BSTriShape');

    if Assigned(original) then begin
      origIndex := original.Index;

      // Copy the block
      copy := nif.CopyBlock(origIndex);

      AddMessage(Format('Copied block %d to new block %d', [origIndex, copy.Index]));
      AddMessage('Original type: ' + original.BlockType);
      AddMessage('Copy type: ' + copy.BlockType);

      // Modify the copy (example)
      if copy.StringsCount > 0 then
        copy.Strings[0].EditValue := copy.Strings[0].EditValue + '_Copy';

      nif.SaveToFile('meshes\clutter\pottery\pot01_duplicated.nif');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
- [TwbNifFile_InsertBlock](TwbNifFile_InsertBlock.md)
- [TwbNifFile_ConvertBlock](TwbNifFile_ConvertBlock.md)
- [TdfElement_Assign](TdfElement_Assign.md)
