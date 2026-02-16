# AddBlock

## Syntax

```pascal
function AddBlock(ABlockType: string): TwbNifBlock;
```

Access via: `nifFile.AddBlock(BlockType)`

## Description

Creates a new block of the specified type and adds it to the end of the NIF file's block list. Returns the newly created block.

This is the primary method for building NIF structures programmatically. The new block is initialized with default values appropriate for its type and can be configured after creation.

The block is added to the end of the block list (before the footer if one exists). If you need to insert a block at a specific position, use InsertBlock instead.

Common block types to add:
- "NiNode" / "BSFadeNode" - Scene graph nodes
- "BSTriShape" - Geometry (Skyrim SE/FO4)
- "NiTriShape" - Geometry (older games)
- "BSLightingShaderProperty" - Material/shader
- "BSShaderTextureSet" - Texture paths
- "NiStringExtraData" - String metadata

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The type of block to create |

## Returns

Returns the newly created block.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  geometry: TwbNifBlock;
  shader: TwbNifBlock;
  texSet: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.NifVersion := nfSSE;

    // Add root node
    rootNode := nif.AddBlock('BSFadeNode');
    rootNode.ElementByPath['Name'].EditValue := 'Scene Root';

    // Add geometry
    geometry := nif.AddBlock('BSTriShape');
    geometry.ElementByPath['Name'].EditValue := 'Mesh';

    // Add shader property
    shader := nif.AddBlock('BSLightingShaderProperty');

    // Add texture set
    texSet := nif.AddBlock('BSShaderTextureSet');
    texSet.ElementByPath['Textures\[0]'].EditValue := 'textures\test\diffuse.dds';

    // Link them together
    // (Would need to set up references properly here)

    AddMessage('Created NIF with ' + IntToStr(nif.BlocksCount) + ' blocks');
    nif.SaveToFile('meshes\test\created_mesh.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_InsertBlock](TwbNifFile_InsertBlock.md)
- [TwbNifFile_CopyBlock](TwbNifFile_CopyBlock.md)
- [TwbNifBlock_AddChild](TwbNifBlock_AddChild.md)
- [TwbNifFile_BlocksCount](TwbNifFile_BlocksCount.md)
