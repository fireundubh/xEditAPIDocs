# UpdateNormals

## Syntax

```pascal
function UpdateNormals(ABlock: TwbNifBlock): Boolean;
function UpdateNormals(ABlock: TwbNifBlock; AAddIfMissing: Boolean): Boolean;
```

## Description

Recalculates vertex normals for this geometry block based on face geometry. Normals are essential for proper lighting in the game engine.

This function:
- Calculates face normals from triangle vertex positions
- Averages face normals at each vertex to create smooth shading
- Updates the Normal vectors in the vertex data
- Optionally adds Normal data if it's missing from the geometry

Normals must be updated whenever you modify vertex positions or triangle topology to ensure correct lighting. Without proper normals, meshes will appear incorrectly lit or completely black.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The geometry block whose normals to update |
| AAddIfMissing | Boolean | Optional. If True, add Normal data if not present. Default is True |

## Returns

Returns True if normals were successfully updated, False if the block doesn't support normals or has no geometry.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  vertex: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\furniture\bench01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Modify vertex positions (example: offset all vertices)
      vertex := geometry.ElementByPath['Vertex Data\[0]\Vertex'];
      vertex.NativeValues['Z'] := vertex.NativeValues['Z'] + 10.0;

      // Recalculate normals for proper lighting
      if UpdateNormals(geometry, True) then begin
        AddMessage('Normals updated successfully');

        // Update bounds as well
        UpdateBounds(geometry);

        nif.SaveToFile('meshes\furniture\bench01_modified.nif');
      end else
        AddMessage('Failed to update normals');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_UpdateTangents](TwbNifBlock_UpdateTangents.md)
- [TwbNifBlock_UpdateBounds](TwbNifBlock_UpdateBounds.md)
- [TwbNifFile_SpellFaceNormals](TwbNifFile_SpellFaceNormals.md)
- [TwbNifFile_SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md)
