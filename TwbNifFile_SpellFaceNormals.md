# SpellFaceNormals

## Syntax

```pascal
function SpellFaceNormals: Boolean;
```

Access via: `nifFile.SpellFaceNormals`

## Description

Recalculates vertex normals for all geometry blocks in the NIF file. Returns True if any geometry was updated.

This is a batch operation that applies UpdateNormals to every geometry block in the file. It's useful when you've modified vertex positions across multiple geometry blocks and need to update all normals at once.

The spell:
- Finds all geometry blocks in the file
- Recalculates face normals from triangle vertex positions
- Updates vertex normals by averaging adjacent face normals
- Adds normal data to geometry that lacks it
- Updates bounds for each modified geometry block

Proper normals are essential for correct lighting. After modifying vertex positions, always recalculate normals before saving.

## Returns

Returns True if any geometry normals were updated, False if no geometry was found or updated.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  geometry: TwbNifBlock;
  vertex: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\furniture\bench01.nif');

    // Modify all geometry (example: scale everything)
    for i := 0 to nif.BlocksCount - 1 do begin
      geometry := nif.Blocks[i];

      if geometry.IsNiObject('NiTriBasedGeom', True) then begin
        // Scale vertices (simplified example)
        vertex := geometry.Elements['Vertex Data\[0]\Vertex'];
        if Assigned(vertex) then begin
          vertex.NativeValues['X'] := vertex.NativeValues['X'] * 1.5;
          vertex.NativeValues['Y'] := vertex.NativeValues['Y'] * 1.5;
          vertex.NativeValues['Z'] := vertex.NativeValues['Z'] * 1.5;
        end;
      end;
    end;

    // Recalculate all normals after modifications
    if nif.SpellFaceNormals then
      AddMessage('Normals updated successfully')
    else
      AddMessage('No geometry to update');

    nif.SaveToFile('meshes\furniture\bench01_scaled.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md)
- [TwbNifFile_SpellAddUpdateTangents](TwbNifFile_SpellAddUpdateTangents.md)
- [TwbNifBlock_UpdateNormals](TwbNifBlock_UpdateNormals.md)
- [TwbNifBlock_UpdateBounds](TwbNifBlock_UpdateBounds.md)
