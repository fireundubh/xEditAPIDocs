# TwbDDSFile.Create

## Syntax

```pascal
function TwbDDSFile.Create: TwbDDSFile;
```

## Description

Creates a new DDS (DirectDraw Surface) file handler instance.

DDS is Microsoft's texture format widely used in video games for efficient GPU texture storage. In Bethesda games, DDS files store all textures including diffuse maps, normal maps, specular maps, and other texture types. The format supports various compression schemes (DXT1, DXT5, BC7, etc.) and mipmap chains for optimal rendering performance.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading DDS headers, accessing texture properties, and extracting or modifying texture data. This is useful for texture analysis, conversion, or validation scripts.

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
    // Load existing texture file
    ddsFile.LoadFromFile('Textures\Architecture\Whiterun\WRBuildings01.dds');

    // Read texture properties
    width := ddsFile.ElementByName('Width', True).NativeValue;
    height := ddsFile.ElementByName('Height', True).NativeValue;
    AddMessage(Format('Texture size: %dx%d', [width, height]));

    // Check compression format
    AddMessage('Format: ' + ddsFile.ElementByName('Format', True).EditValue);
    AddMessage('Mipmap count: ' + ddsFile.ElementByName('Mipmap Count', True).EditValue);
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
