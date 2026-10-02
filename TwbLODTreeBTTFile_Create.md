# TwbLODTreeBTTFile.Create

## Syntax

```pascal
function TwbLODTreeBTTFile.Create: TwbLODTreeBTTFile;
```

## Description

Creates a new tree LOD reference-block handler.

Skyrim and Skyrim Special Edition store these as `.btt` files under `meshes\terrain\<Worldspace>\trees\`. Fallout 3 and New Vegas use the same record with a `.dtl` extension. The file is an array of tree types. Each type has a `Type` index into the LST and a `References` array of placements (`X`, `Y`, `Z`, `Rotation`, `Scale`, `FormID`). It is not a texture atlas. Billboard images are separate DDS files. The LST file holds each tree type's width, height, and atlas UVs.

The created instance inherits from `TdfElement`. After creation, use `LoadFromFile` to read an existing block.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODTreeBTTFile` instance ready for loading or creating a tree LOD reference block.

## Example

```pascal
var
  bttFile: TwbLODTreeBTTFile;
  treeEntry: TdfElement;
begin
  bttFile := TwbLODTreeBTTFile.Create;
  try
    // LOD level, cell X, cell Y
    bttFile.LoadFromFile('meshes\terrain\Tamriel\trees\Tamriel.4.0.0.btt');

    AddMessage(Format('Tree types: %d', [bttFile.Count]));
    if bttFile.Count > 0 then begin
      treeEntry := bttFile.Items[0];
      AddMessage('Type: ' + treeEntry.EditValues['Type']);
      AddMessage('First X: ' + treeEntry.EditValues['References\[0]\X']);
      AddMessage('First Y: ' + treeEntry.EditValues['References\[0]\Y']);
      AddMessage('First Z: ' + treeEntry.EditValues['References\[0]\Z']);
    end;
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
