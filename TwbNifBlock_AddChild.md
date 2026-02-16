# AddChild

## Syntax

```pascal
function AddChild(ABlockType: string): TwbNifBlock;
```

**Access via:** `block.AddChild(ABlockType)`

## Description

Adds a new child block to this NIF block and returns the created block. This is used to build the NIF scene graph hierarchy by attaching child nodes and geometry to parent nodes.

This method only works on blocks that support children (typically NiNode and derived types). It creates a new block of the specified type, adds it to the NIF file, and establishes the parent-child relationship by updating the parent's Children array.

The new child block is properly initialized with default values and can be further configured after creation. The method handles all the necessary internal bookkeeping including updating block references and counts.

## Parameters

| Name | Type | Description |
|------|------|-------------|
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
    childNode := rootNode.AddChild('NiNode');

    // Set the child node's name
    childNode.EditValues['Name'] := 'ChildNode01';

    // Add geometry as a child of the child node
    geometry := childNode.AddChild('BSTriShape');

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
