# SpellTriangulate

## Syntax

```pascal
function SpellTriangulate: Boolean;
```

Access via: `nifFile.SpellTriangulate`

## Description

Converts all triangle strip geometry in the NIF file to triangle list format. Returns True if any geometry was converted.

Triangle strips are an older, more compact way of storing geometry that uses fewer indices by sharing vertices between adjacent triangles. Triangle lists store each triangle independently with three explicit indices.

This spell:
- Finds all geometry blocks using triangle strips (NiTriStrips, BSTriStrips)
- Converts the strip data to independent triangles
- Updates the geometry block's structure
- Preserves all other geometry data (vertices, normals, UVs, etc.)

Converting to triangles is often necessary when:
- Preparing meshes for editing or manipulation
- Ensuring compatibility with tools that don't support strips
- Making geometry data easier to work with programmatically

## Returns

Returns True if any geometry was triangulated, False if no triangle strips were found.

## Example

```pascal
var
  nif: TwbNifFile;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\common\cup01.nif');

    AddMessage('Original block count: ' + IntToStr(nif.BlocksCount));

    // Convert all triangle strips to triangles
    if nif.SpellTriangulate then begin
      AddMessage('Successfully triangulated geometry');

      // Update normals and tangents after triangulation
      nif.SpellFaceNormals;
      nif.SpellUpdateTangents;

      nif.SaveToFile('meshes\clutter\common\cup01_triangulated.nif');
    end else
      AddMessage('No triangle strips found');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_SpellFaceNormals](TwbNifFile_SpellFaceNormals.md)
- [TwbNifFile_SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md)
- [TwbNifBlock_UpdateBounds](TwbNifBlock_UpdateBounds.md)
