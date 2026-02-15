# SpellUpdateTangents

## Syntax

```pascal
function SpellUpdateTangents(ANifFile: TwbNifFile): Boolean;
```

## Description

Recalculates tangent and bitangent vectors for all geometry blocks in the NIF file that already have tangent data. Returns True if any geometry was updated.

This is a batch operation that applies UpdateTangents to every geometry block in the file that already has tangent vectors. It will not add tangent data to geometry that lacks it (use SpellAddUpdateTangents for that).

The spell:
- Finds all geometry blocks with existing tangent data
- Recalculates tangent and bitangent vectors from vertices, normals, and UVs
- Updates the tangent space vectors
- Skips geometry that doesn't have tangent data

Tangent space is essential for normal mapping. After modifying vertices, normals, or UVs, you must update tangents for normal maps to display correctly.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ANifFile | TwbNifFile | The NIF file object |

## Returns

Returns True if any geometry tangents were updated, False if no geometry with tangents was found.

## Example

```pascal
var
  nif: TwbNifFile;
  i: Integer;
  geometry: TwbNifBlock;
  uv: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    // Modify UV coordinates across all geometry
    for i := 0 to nif.BlocksCount - 1 do begin
      geometry := nif.Blocks[i];

      if IsNiObject(geometry, 'NiTriBasedGeom', True) then begin
        uv := geometry.ElementByPath['Vertex Data\[0]\UV'];
        if Assigned(uv) then begin
          uv.NativeValues['U'] := uv.NativeValues['U'] * 2.0;
          uv.NativeValues['V'] := uv.NativeValues['V'] * 2.0;
        end;
      end;
    end;

    // Recalculate all normals and tangents
    nif.SpellFaceNormals;

    if nif.SpellUpdateTangents then
      AddMessage('Tangents updated successfully')
    else
      AddMessage('No geometry with tangents found');

    nif.SaveToFile('meshes\armor\iron\ironarmor_scaled_uvs.nif');
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_SpellAddUpdateTangents](TwbNifFile_SpellAddUpdateTangents.md)
- [TwbNifFile_SpellFaceNormals](TwbNifFile_SpellFaceNormals.md)
- [TwbNifBlock_UpdateTangents](TwbNifBlock_UpdateTangents.md)
- [TwbNifBlock_UpdateNormals](TwbNifBlock_UpdateNormals.md)
