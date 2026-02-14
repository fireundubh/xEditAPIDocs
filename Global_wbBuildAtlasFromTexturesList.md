# wbBuildAtlasFromTexturesList

## Syntax

```pascal
procedure wbBuildAtlasFromTexturesList(ATextures: TStrings; AMaxTextureSize: Integer; AMaxTileSize: Integer; AAtlasWidth: Integer; AAtlasHeight: Integer; AAtlasFileName: string; AAtlasMapFileName: string);
```

## Description

Builds a texture atlas from a list of texture files, combining multiple textures into a single large texture with specified dimensions. This is used for LOD generation to optimize texture memory usage.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ATextures | TStrings | String list containing paths to the textures to include in the atlas |
| AMaxTextureSize | Integer | Maximum size for individual textures before downscaling |
| AMaxTileSize | Integer | Maximum size for individual tiles in the atlas |
| AAtlasWidth | Integer | Width of the output atlas texture |
| AAtlasHeight | Integer | Height of the output atlas texture |
| AAtlasFileName | string | Output filename for the atlas texture |
| AAtlasMapFileName | string | Output filename for the atlas mapping file |

## Returns

This function does not return a value.

## Example

```pascal
var
  textureList: TStringList;
begin
  textureList := TStringList.Create;
  try
    textureList.Add('textures\landscape\grass01.dds');
    textureList.Add('textures\landscape\grass02.dds');
    textureList.Add('textures\landscape\grass03.dds');

    wbBuildAtlasFromTexturesList(textureList, 512, 256, 2048, 2048,
                                  'LOD_Atlas.dds', 'LOD_Atlas_Map.txt');

    AddMessage('Atlas created with ' + IntToStr(textureList.Count) + ' textures');
  finally
    textureList.Free;
  end;
end;
```

## See Also

- [wbBuildAtlasFromAtlasMap](Global_wbBuildAtlasFromAtlasMap.md)
- [wbGetUVRangeTexturesList](Global_wbGetUVRangeTexturesList.md)
