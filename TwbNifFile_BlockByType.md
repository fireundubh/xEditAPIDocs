# BlockByType

## Syntax

```pascal
function BlockByType(ABlockType: string): TwbNifBlock;
function BlockByType(ABlockType: string; AInherited: Boolean): TwbNifBlock;
```

Access via: `nifFile.BlockByType(BlockType)` or `nifFile.BlockByType(BlockType, Inherited)`

## Description

Finds and returns the first block of the specified type in the NIF file. Returns nil if no matching block is found.

This method searches through all blocks in the file and returns the first one that matches the type criteria. It's useful when you know there's only one block of a particular type, or when you only need to find the first occurrence.

The function supports both exact type matching and inheritance checking. When inheritance is enabled, it returns the first block that is of the specified type or inherits from it.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The block type to search for |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

Returns the first matching block, or nil if none found.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  shader: TwbNifBlock;
  rootNode: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    // Find the first geometry block (with inheritance)
    geometry := nif.BlockByType('NiTriBasedGeom', True);

    if Assigned(geometry) then begin
      AddMessage('Found geometry: ' + geometry.BlockType);

      // Get its shader
      shader := geometry.PropertyByType('BSLightingShaderProperty');
      if Assigned(shader) then
        AddMessage('Has lighting shader');
    end else
      AddMessage('No geometry found');

    // Find root node (exact match)
    rootNode := nif.BlockByType('NiNode', False);

    if Assigned(rootNode) then
      AddMessage('Root node: ' + rootNode.EditValues['Name']);
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_BlocksByType](TwbNifFile_BlocksByType.md)
- [TwbNifFile_BlockByName](TwbNifFile_BlockByName.md)
- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
- [TwbNifBlock_IsNiObject](TwbNifBlock_IsNiObject.md)
