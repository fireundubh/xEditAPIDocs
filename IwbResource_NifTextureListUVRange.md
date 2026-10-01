# NifTextureListUVRange

## Syntax

```pascal
function NifTextureListUVRange(AData: TBytes; AUVRange: Single; AList: TStrings): Boolean;
```

## Description

Clears `AList` and fills it with textures from `NiTriShape` blocks whose UV coordinates all stay inside `-AUVRange` to `AUVRange`. A shape with any UV outside that range is skipped, so tiled shapes are left out. Only a BSLightingShaderProperty texture set on that shape is listed. Empty paths are removed.

A nil list or an empty `AData` returns False. A NIF that loads returns True even when the list is empty.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The raw binary data of the NIF file |
| AUVRange | Single | Absolute UV limit. A coordinate past `-AUVRange` or `AUVRange` drops that shape |
| AList | TStrings | List cleared and filled with textures from shapes inside the range |

## Returns

True when the NIF loaded. False when `AList` is nil, `AData` is empty, or the NIF did not load.

## Example

```pascal
var
  nifData: TBytes;
  textures: TStringList;
begin
  textures := TStringList.Create;
  try
    nifData := ResourceOpenData('', 'meshes\landscape\mountains\mountaincliff01.nif');

    if NifTextureListUVRange(nifData, 1.0, textures) then
      AddMessage('Textures on shapes inside UV 1.0: ' + IntToStr(textures.Count));
  finally
    textures.Free;
  end;
end;
```

## See Also

- [NifTextureList](IwbResource_NifTextureList.md)
- [wbGetUVRangeTexturesList](Global_wbGetUVRangeTexturesList.md)
