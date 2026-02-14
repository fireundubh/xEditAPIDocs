# NifTextureListUVRange

## Syntax

```pascal
function NifTextureListUVRange(aData: TBytes; aUVRange: Single; aList: TStrings): Boolean;
```

## Description

Extracts texture file paths from a NIF mesh file that have UV coordinates exceeding a specified range. This is useful for identifying textures that use tiling or have UV mapping outside the standard 0.0-1.0 range.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aData | TBytes | The raw binary data of the NIF file |
| aUVRange | Single | The UV range threshold to check against |
| aList | TStrings | The string list to receive the texture paths that exceed the UV range |

## Returns

Returns True if the NIF was successfully parsed, False otherwise.

## Example

```pascal
var
  nifData: TBytes;
  tiledTextures: TStringList;
begin
  tiledTextures := TStringList.Create;
  try
    nifData := ResourceOpenData('', 'meshes\landscape\mountains\mountaincliff01.nif');

    // Find textures with UV coordinates exceeding 1.0
    if NifTextureListUVRange(nifData, 1.0, tiledTextures) then
      AddMessage('Found ' + IntToStr(tiledTextures.Count) + ' tiled textures');
  finally
    tiledTextures.Free;
  end;
end;
```

## See Also

- [NifTextureList](IwbResource_NifTextureList.md)
- [wbGetUVRangeTexturesList](Global_wbGetUVRangeTexturesList.md)
