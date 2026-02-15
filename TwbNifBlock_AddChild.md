# AddChild

## Syntax

```pascal
function AddChild(ABlock: TwbNifBlock; ABlockType: string): TwbNifBlock;
```

## Description

Adds a new child block to this NIF block and returns the created block. This is used to build the NIF scene graph hierarchy by attaching child nodes and geometry to parent nodes.

This function only works on blocks that support children (typically NiNode and derived types). It creates a new block of the specified type, adds it to the NIF file, and establishes the parent-child relationship by updating the parent's Children array.

The new child block is properly initialized with default values and can be further configured after creation. The function handles all the necessary internal bookkeeping including updating block references and counts.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The parent block that will receive the new child |
| ABlockType | string | The type of block to create (e.g., "NiNode", "BSTriShape") |

## Returns

Returns the newly created child block.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  childNode: TwbNifBlock;
  geometry: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.NifVersion := nfSSE;

    // Create root node
    rootNode := nif.AddBlock('NiNode');

    // Add a child node to the root
    childNode := AddChild(rootNode, 'NiNode');

    // Set the child node's name
    childNode.ElementByPath['Name'].EditValue := 'ChildNode01';

    // Add geometry as a child of the child node
    geometry := AddChild(childNode, 'BSTriShape');

    AddMessage('Created hierarchy: Root -> ChildNode01 -> BSTriShape');

    nif.SaveToFile('meshes\test\custom_hierarchy.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_AddExtraData](TwbNifBlock_AddExtraData.md)
- [TwbNifBlock_AddProperty](TwbNifBlock_AddProperty.md)
- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
- [TwbNifFile_AddBlock](TwbNifFile_AddBlock.md)
