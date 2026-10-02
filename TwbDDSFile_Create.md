# TwbDDSFile.Create

## Syntax

```pascal
function TwbDDSFile.Create: TwbDDSFile;
```

## Description

Creates a new DDS (DirectDraw Surface) file handler instance.

DDS is Microsoft's texture format widely used in video games for efficient GPU texture storage. In Bethesda games, DDS files store all textures including diffuse maps, normal maps, specular maps, and other texture types. The format supports various compression schemes (DXT1, DXT5, BC7, etc.) and mipmap chains for optimal rendering performance.

The created instance inherits from `TdfElement`. The definition covers the DDS header (dimensions, mip count, and pixel format under `HEADER`), not the image bytes.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbDDSFile` instance ready for loading or creating DDS texture data.

## Example

```pascal
var
  ddsFile: TwbDDSFile;
  width, height: Integer;
begin
  ddsFile := TwbDDSFile.Create;
  try
    ddsFile.LoadFromFile('Textures\Architecture\Whiterun\WRBuildings01.dds');

    width := ddsFile.NativeValues['HEADER\dwWidth'];
    height := ddsFile.NativeValues['HEADER\dwHeight'];
    AddMessage(Format('Texture size: %dx%d', [width, height]));

    AddMessage('FourCC: ' + ddsFile.EditValues['HEADER\ddspf\dwFourCC']);
    AddMessage('Mipmap count: ' + ddsFile.EditValues['HEADER\dwMipMapCount']);
  finally
    ddsFile.Free;
  end;
end;
```

## See Also

- [wbDDSDataToBitmap](IwbResource_wbDDSDataToBitmap.md)
- [wbDDSResourceToBitmap](IwbResource_wbDDSResourceToBitmap.md)
- [wbDDSStreamToBitmap](IwbResource_wbDDSStreamToBitmap.md)
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_ElementByName](TdfElement_ElementByName.md)
