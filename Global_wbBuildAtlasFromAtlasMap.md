# wbBuildAtlasFromAtlasMap

## Syntax

```pascal
procedure wbBuildAtlasFromAtlasMap(aAtlasMap: TStrings; aBrightness: Single; aGammaR: Single; aGammaG: Single; aGammaB: Single);
```

## Description

Builds a texture atlas from an atlas map specification, applying brightness and gamma correction values to the RGB channels. This function reconstructs a texture atlas using the mapping information and color adjustments.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aAtlasMap | TStrings | String list containing the atlas map specification |
| aBrightness | Single | Brightness adjustment value to apply |
| aGammaR | Single | Gamma correction value for the red channel |
| aGammaG | Single | Gamma correction value for the green channel |
| aGammaB | Single | Gamma correction value for the blue channel |

## Returns

This function does not return a value.

## Example

```pascal
var
  atlasMap: TStringList;
begin
  atlasMap := TStringList.Create;
  try
    atlasMap.LoadFromFile(DataPath + 'LODGen\atlas_map.txt');

    // Build atlas with default brightness and gamma
    wbBuildAtlasFromAtlasMap(atlasMap, 1.0, 1.0, 1.0, 1.0);

    AddMessage('Atlas built from map');
  finally
    atlasMap.Free;
  end;
end;
```

## See Also

- [wbBuildAtlasFromTexturesList](Global_wbBuildAtlasFromTexturesList.md)
