# SpellAddUpdateTangents

## Syntax

```pascal
function SpellAddUpdateTangents(ANifFile: TwbNifFile): Boolean;
```

## Description

Adds tangent and bitangent vectors to all geometry blocks that lack them, and updates tangents for geometry that already has them. Returns True if any geometry was processed.

This is a batch operation that applies UpdateTangents with the add-if-missing flag to every geometry block in the file. It's more comprehensive than SpellUpdateTangents because it will add tangent data to geometry that doesn't have it.

The spell:
- Finds all geometry blocks in the file
- Adds tangent data to geometry that lacks it
- Updates tangent data for geometry that already has it
- Calculates tangent and bitangent vectors from vertices, normals, and UVs
- Skips geometry that lacks the required data (normals or UVs)

Use this when:
- Preparing meshes for use with normal maps
- Converting old meshes to support modern shaders
- Ensuring all geometry has proper tangent space

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |

## Returns

Returns True if any geometry tangents were added or updated, False if no geometry was processed.

## Example

```pascal
var
  nif: TwbNifFile;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\bucket01.nif');

    // Ensure all geometry has proper normals first
    nif.SpellFaceNormals;

    // Add tangents to all geometry for normal mapping support
    if nif.SpellAddUpdateTangents then begin
      AddMessage('Tangent space added/updated for all geometry');
      nif.SaveToFile('meshes\clutter\bucket01_with_tangents.nif');
    end else
      AddMessage('Failed to add/update tangents');
  finally
    nif.Free;
  end;
end;
```

## Example (Modernizing Old Mesh)

```pascal
var
  nif: TwbNifFile;
begin
  nif := TwbNifFile.Create;
  try
    // Load an old Oblivion mesh
    nif.LoadFromFile('meshes\oblivion\architecture\house01.nif');

    AddMessage('Modernizing mesh...');

    // Convert strips to triangles
    nif.SpellTriangulate;

    // Recalculate normals
    nif.SpellFaceNormals;

    // Add tangent space for normal mapping
    if nif.SpellAddUpdateTangents then
      AddMessage('Mesh modernized successfully');

    nif.SaveToFile('meshes\oblivion\architecture\house01_modernized.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md)
- [TwbNifFile_SpellFaceNormals](TwbNifFile_SpellFaceNormals.md)
- [TwbNifBlock_UpdateTangents](TwbNifBlock_UpdateTangents.md)
- [TwbNifFile_SpellTriangulate](TwbNifFile_SpellTriangulate.md)
