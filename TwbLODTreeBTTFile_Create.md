# TwbLODTreeBTTFile.Create

## Syntax

```pascal
function TwbLODTreeBTTFile.Create: TwbLODTreeBTTFile;
```

## Description

Creates a new BTT (Billboard Tree) file handler instance.

BTT files store billboard texture atlases used for rendering distant trees in Bethesda games' LOD system. They contain packed texture data showing tree silhouettes from multiple angles, allowing efficient rendering of tree canopies at long distances. BTT files work together with LST (tree list) files to provide the complete tree LOD rendering system.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods. After creation, use `LoadFromFile` to read an existing billboard tree texture, typically for analysis or conversion purposes.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODTreeBTTFile` instance ready for loading or creating billboard tree texture data.

## Example

```pascal
var
  bttFile: TwbLODTreeBTTFile;
begin
  bttFile := TwbLODTreeBTTFile.Create;
  try
    // Load billboard tree texture atlas
    bttFile.LoadFromFile('Textures\Terrain\LODGen\TreePineForest01.btt');

    // Access BTT properties
    AddMessage('Width: ' + bttFile.ElementByName('Width', True).EditValue);
    AddMessage('Height: ' + bttFile.ElementByName('Height', True).EditValue);
    AddMessage('Format: ' + bttFile.ElementByName('Format', True).EditValue);
  finally
    bttFile.Free;
  end;
end;
```

## See Also

- [TwbLODTreeLSTFile.Create](TwbLODTreeLSTFile_Create.md) - Tree list file
- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_ElementByName](TdfElement_ElementByName.md)
