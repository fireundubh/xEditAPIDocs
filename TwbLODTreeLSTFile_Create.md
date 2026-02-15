# TwbLODTreeLSTFile.Create

## Syntax

```pascal
function TwbLODTreeLSTFile.Create: TwbLODTreeLSTFile;
```

## Description

Creates a new LOD Tree List file handler instance.

LST files are used in Bethesda games to define tree object placement and properties for distant terrain LOD (Level of Detail). They contain lists of tree references with positions, scales, and tree type information. These files work in conjunction with BTT (Billboard Tree) files to provide efficient rendering of distant vegetation.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods. After creation, use `LoadFromFile` to read an existing tree list, or build the tree structure programmatically for LOD generation scripts.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbLODTreeLSTFile` instance ready for loading or creating tree LOD list data.

## Example

```pascal
var
  lstFile: TwbLODTreeLSTFile;
  treeEntry: TdfElement;
begin
  lstFile := TwbLODTreeLSTFile.Create;
  try
    // Load existing tree list for a worldspace cell
    lstFile.LoadFromFile('Meshes\Terrain\Tamriel\Trees\Tamriel.4.-3.lst');

    // Iterate through tree entries
    AddMessage(Format('Tree count: %d', [lstFile.Count]));

    // Access individual tree data
    if lstFile.Count > 0 then begin
      treeEntry := lstFile.Elements[0];
      AddMessage('Tree type: ' + treeEntry.ElementByName('Type', True).EditValue);
      AddMessage('Position: ' + treeEntry.ElementByName('Position', True).EditValue);
    end;
  finally
    lstFile.Free;
  end;
end;
```

## See Also

- [TwbLODTreeBTTFile.Create](TwbLODTreeBTTFile_Create.md) - Billboard tree texture file
- [GenerateLODTES5Trees](Global_GenerateLODTES5Trees.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_Count](TdfElement_Count.md)
