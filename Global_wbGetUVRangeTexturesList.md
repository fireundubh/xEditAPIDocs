# wbGetUVRangeTexturesList

## Syntax

```pascal
procedure wbGetUVRangeTexturesList(AMeshes: TStrings; ATextures: TStrings; AUVRange: Single);
```

## Description

Analyzes a list of mesh files and builds a list of textures that use UV coordinates exceeding a specified range. This is useful for identifying tiling textures used in LOD generation.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AMeshes | TStrings | String list containing paths to mesh files to analyze |
| ATextures | TStrings | Output string list to receive texture paths that exceed the UV range |
| AUVRange | Single | The UV range threshold to check against |

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

    // Find textures with UV > 1.0 (tiling textures)
    wbGetUVRangeTexturesList(meshList, textureList, 1.0);

    AddMessage('Found ' + IntToStr(textureList.Count) + ' tiling textures');
  finally
    meshList.Free;
    textureList.Free;
  end;
end;
```

## See Also

- [NifTextureListUVRange](IwbResource_NifTextureListUVRange.md)
- [wbBuildAtlasFromTexturesList](Global_wbBuildAtlasFromTexturesList.md)
