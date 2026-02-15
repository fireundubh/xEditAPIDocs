# BlockType

## Syntax

```pascal
function BlockType(ABlock: TwbNifBlock): string;
```

## Description

Returns the block type name of a NIF block. The block type identifies what kind of NIF object this block represents (e.g., "NiNode", "NiTriShape", "BSLightingShaderProperty", etc.).

NIF files are composed of blocks that form a hierarchical structure. Each block has a specific type that determines its purpose and data structure. Common block types include:
- **NiNode**: Scene graph nodes that can have children
- **NiTriShape/BSTriShape**: Geometry blocks containing mesh data
- **NiTriStrips/BSTriStrips**: Geometry using triangle strips
- **BSLightingShaderProperty**: Shader properties for materials
- **NiSkinInstance**: Skinning data for animated meshes
- **bhkCollisionObject**: Collision data

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The NIF block to query |

## Returns

Returns the block type name as a string.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  block: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrterrain01.nif');

    AddMessage('NIF contains ' + IntToStr(nif.BlocksCount) + ' blocks:');

    for i := 0 to nif.BlocksCount - 1 do begin
      block := nif.Blocks[i];
      AddMessage('Block ' + IntToStr(i) + ': ' + BlockType(block));
    end;
    // Example output:
    // Block 0: NiNode
    // Block 1: BSLightingShaderProperty
    // Block 2: BSShaderTextureSet
    // Block 3: BSTriShape
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_IsNiObject](TwbNifBlock_IsNiObject.md)
- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
- [TwbNifFile_BlocksByType](TwbNifFile_BlocksByType.md)
- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
