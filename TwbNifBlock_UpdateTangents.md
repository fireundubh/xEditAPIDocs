# UpdateTangents

## Syntax

```pascal
function UpdateTangents(ABlock: TwbNifBlock): Boolean;
function UpdateTangents(ABlock: TwbNifBlock; AAddIfMissing: Boolean): Boolean;
```

## Description

Recalculates tangent and bitangent vectors for this geometry block based on normals and texture coordinates. Tangent space is required for normal mapping to work correctly.

This function:
- Calculates tangent and bitangent vectors from vertex positions, normals, and UV coordinates
- Updates the Tangent and Bitangent vectors in the vertex data
- Optionally adds tangent data if it's missing from the geometry
- Is essential for meshes that use normal maps (nearly all modern game meshes)

Tangents must be updated whenever you modify vertex positions, normals, or UV coordinates. Without proper tangents, normal maps will not display correctly, causing incorrect surface detail rendering.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The geometry block whose tangents to update |
| AAddIfMissing | Boolean | Optional. If True, add tangent data if not present. Default is True |

## Returns

Returns True if tangents were successfully updated, False if the block doesn't support tangents, has no geometry, or lacks required data (normals, UVs).

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  uv: TdfElement;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Modify UV coordinates
      uv := geometry.ElementByPath['Vertex Data\[0]\UV'];
      uv.NativeValues['U'] := uv.NativeValues['U'] * 2.0;
      uv.NativeValues['V'] := uv.NativeValues['V'] * 2.0;

      // Must update normals first, then tangents
      if UpdateNormals(geometry, True) then begin
        if UpdateTangents(geometry, True) then begin
          AddMessage('Tangent space updated successfully');
          UpdateBounds(geometry);
          nif.SaveToFile('meshes\armor\iron\ironarmor_modified.nif');
        end else
          AddMessage('Failed to update tangents');
      end;
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_UpdateNormals](TwbNifBlock_UpdateNormals.md)
- [TwbNifBlock_UpdateBounds](TwbNifBlock_UpdateBounds.md)
- [TwbNifFile_SpellUpdateTangents](TwbNifFile_SpellUpdateTangents.md)
- [TwbNifFile_SpellAddUpdateTangents](TwbNifFile_SpellAddUpdateTangents.md)
