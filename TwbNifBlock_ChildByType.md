# ChildByType

## Syntax

```pascal
function ChildByType(ABlock: TwbNifBlock; ABlockType: string): TwbNifBlock;
function ChildByType(ABlock: TwbNifBlock; ABlockType: string; AInherited: Boolean): TwbNifBlock;
```

## Description

Finds and returns the first child block of a specific type. Returns nil if no matching child is found.

This is a convenience method for finding a single child when you expect only one or only need the first match. It searches the block's Children array and returns the first block that matches the type criteria.

The function supports both exact type matching and inheritance checking. When inheritance is enabled, it returns the first child that is of the specified type or inherits from it.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The parent block whose children to search |
| ABlockType | string | The block type to search for |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

Returns the first matching child block, or nil if none found.

## Example

```pascal
var
  nif: TwbNifFile;
  rootNode: TwbNifBlock;
  geometry: TwbNifBlock;
  childNode: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\ruins\ruinspot02.nif');

    rootNode := nif.RootNode;

    if Assigned(rootNode) then begin
      // Find the first geometry child
      geometry := ChildByType(rootNode, 'NiTriBasedGeom', True);

      if Assigned(geometry) then
        AddMessage('Found geometry: ' + BlockType(geometry))
      else
        AddMessage('No geometry found');

      // Find a specific child node type
      childNode := ChildByType(rootNode, 'NiNode', False);

      if Assigned(childNode) then
        AddMessage('Found NiNode child: ' + childNode.ElementByPath['Name'].EditValue);
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_ChildrenByType](TwbNifBlock_ChildrenByType.md)
- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [TwbNifBlock_ExtraDataByType](TwbNifBlock_ExtraDataByType.md)
- [TwbNifFile_BlockByType](TwbNifFile_BlockByType.md)
