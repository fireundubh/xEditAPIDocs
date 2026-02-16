# UpdateBounds

## Syntax

```pascal
function UpdateBounds(): Boolean;
```

**Access via:** `block.UpdateBounds()`

## Description

Recalculates and updates the bounding sphere and bounding box for this geometry block based on its current vertex positions. Returns True if the bounds were successfully updated.

Bounding volumes are used by the game engine for frustum culling and collision detection optimization. When you modify vertex positions, you must update the bounds to ensure proper rendering and collision behavior.

This method:
- Calculates the axis-aligned bounding box from all vertices
- Computes the bounding sphere that encompasses all vertices
- Updates the block's Bounds or Bounding Box fields
- Works on geometry blocks like NiTriShape, BSTriShape, and similar types

## Parameters

None.

## Returns

Returns True if bounds were successfully updated, False if the block doesn't support bounds or has no vertices.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  vertexData: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\barrel01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Modify vertex positions
      vertexData := geometry.ElementByPath['Vertex Data\[0]\Vertex'];
      vertexData.NativeValues['X'] := vertexData.NativeValues['X'] * 2.0;
      vertexData.NativeValues['Y'] := vertexData.NativeValues['Y'] * 2.0;
      vertexData.NativeValues['Z'] := vertexData.NativeValues['Z'] * 2.0;

      // Update bounds to reflect the changes
      if geometry.UpdateBounds() then
        AddMessage('Bounding sphere updated successfully')
      else
        AddMessage('Failed to update bounds');

      nif.SaveToFile('meshes\clutter\barrel01_scaled.nif');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_UpdateNormals](TwbNifBlock_UpdateNormals.md)
- [TwbNifBlock_UpdateTangents](TwbNifBlock_UpdateTangents.md)
- [TwbNifFile_SpellFaceNormals](TwbNifFile_SpellFaceNormals.md)
