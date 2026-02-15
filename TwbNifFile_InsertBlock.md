# InsertBlock

## Syntax

```pascal
function InsertBlock(ANifFile: TwbNifFile; Index: Integer; ABlockType: string): TwbNifBlock;
```

## Description

Creates a new block of the specified type and inserts it at the given position in the NIF file's block list. Returns the newly created block.

This method is similar to AddBlock but allows you to specify where in the block list the new block should be placed. All blocks at the insertion point and after are shifted down by one index.

When you insert a block, all block references (NiRef and NiPtr values) throughout the file are automatically updated to account for the index change. This ensures the file structure remains valid.

Be careful when inserting blocks into loaded files, as the block order can be important for NIF file integrity. Typically, you should insert blocks near related blocks or use the higher-level methods like AddChild or AddProperty when possible.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |
| Index | Integer | The position where the block should be inserted |
| ABlockType | string | The type of block to create |

## Returns

Returns the newly created block.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  newNode: TwbNifBlock;
  insertPos: Integer;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\bucket01.nif');

    rootNode := nif.RootNode;

    // Insert a new node right after the root node
    insertPos := rootNode.Index + 1;
    newNode := nif.InsertBlock(insertPos, 'NiNode');
    newNode.ElementByPath['Name'].EditValue := 'Inserted Node';

    AddMessage(Format('Inserted block at position %d', [insertPos]));
    AddMessage('New block count: ' + IntToStr(nif.BlocksCount));

    nif.SaveToFile('meshes\clutter\bucket01_inserted.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
- [TwbNifFile_CopyBlock](TwbNifFile_CopyBlock.md)
- [TdfElement_Delete](TdfElement_Delete.md)
- [TdfElement_Move](TdfElement_Move.md)
