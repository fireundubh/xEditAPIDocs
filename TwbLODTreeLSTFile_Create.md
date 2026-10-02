# TwbLODTreeLSTFile.Create

## Syntax

```pascal
function TwbLODTreeLSTFile.Create: TwbLODTreeLSTFile;
```

## Description

Creates a new tree LOD index (`.lst`) handler.

Skyrim stores one list per worldspace at `Meshes\Terrain\<Worldspace>\Trees\<Worldspace>.lst`. Fallout 3 and New Vegas use `Meshes\Landscape\LOD\<Worldspace>\Trees\TreeTypes.lst`. Each entry is a tree type: `Type`, `Width`, `Height`, and atlas UV bounds under `Atlas Position`. Placed references (position, rotation, scale, FormID) are in the `.btt` or `.dtl` block files, not in the LST.

The created instance inherits from `TdfElement`. After creation, use `LoadFromFile` to read an existing list.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODTreeLSTFile` instance ready for loading or creating a tree LOD index.

## Example

```pascal
var
  lstFile: TwbLODTreeLSTFile;
  treeEntry: TdfElement;
begin
  lstFile := TwbLODTreeLSTFile.Create;
  try
    lstFile.LoadFromFile('Meshes\Terrain\Tamriel\Trees\Tamriel.lst');

    AddMessage(Format('Tree types: %d', [lstFile.Count]));

    if lstFile.Count > 0 then begin
      treeEntry := lstFile.Items[0];
      AddMessage('Type: ' + treeEntry.EditValues['Type']);
      AddMessage('Width: ' + treeEntry.EditValues['Width']);
      AddMessage('Height: ' + treeEntry.EditValues['Height']);
    end;
  finally
    lstFile.Free;
  end;
end;
```

## See Also

- [TwbLODTreeBTTFile.Create](TwbLODTreeBTTFile_Create.md) - Tree LOD reference block
- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_Count](TdfElement_Count.md)
