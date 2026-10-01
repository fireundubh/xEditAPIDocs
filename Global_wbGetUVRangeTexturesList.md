# wbGetUVRangeTexturesList

## Syntax

```pascal
procedure wbGetUVRangeTexturesList(AMeshes: TStrings; ATextures: TStrings; AUVRange: Single);
```

## Description

Builds the texture list used for an LOD atlas. For each mesh, a shape whose UV coordinates all stay inside `-AUVRange` to `AUVRange` contributes its diffuse texture. A shape with any UV outside that range is skipped, so tiled shapes are left out. UV values outside `-100` to `100` are ignored as bad data and do not count as tiled.

A `.dds` entry in `AMeshes` is added as-is and marked as a billboard. Other names are resolved as mesh resources. A missing mesh is skipped. Texture names are normalized, and a name already in `ATextures` is not added again. A nil list returns without doing anything.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMeshes | TStrings | Mesh paths to scan, or a `.dds` path to add as a billboard |
| ATextures | TStrings | List that receives textures from shapes inside the UV range |
| AUVRange | Single | Absolute UV limit. A coordinate past `-AUVRange` or `AUVRange` drops that shape |

## Returns

This function does not return a value.

## Example

```pascal
var
  meshList, textureList: TStringList;
begin
  meshList := TStringList.Create;
  textureList := TStringList.Create;
  try
    meshList.Add('meshes\landscape\mountains\mountain01.nif');
    meshList.Add('meshes\landscape\rocks\rock01.nif');

    wbGetUVRangeTexturesList(meshList, textureList, 1.0);

    AddMessage('Textures on shapes inside UV 1.0: ' + IntToStr(textureList.Count));
  finally
    meshList.Free;
    textureList.Free;
  end;
end;
```

## See Also

- [NifTextureListUVRange](IwbResource_NifTextureListUVRange.md)
- [wbBuildAtlasFromTexturesList](Global_wbBuildAtlasFromTexturesList.md)
