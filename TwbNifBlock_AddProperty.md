# AddProperty

## Syntax

```pascal
function AddProperty(ABlockType: string): TwbNifBlock;
```

**Access via:** `block.AddProperty(ABlockType)`

## Description

Adds a new property block to this NIF block and returns the created block. Property blocks control rendering and material characteristics of geometry and nodes.

Properties define how objects are rendered in the game engine. Common property types include:
- **BSLightingShaderProperty**: Controls lighting, textures, and shader parameters (Skyrim/FO4)
- **BSEffectShaderProperty**: Special effects shaders (glow, parallax)
- **NiAlphaProperty**: Alpha blending and transparency settings
- **NiMaterialProperty**: Material colors and properties (older games)
- **BSShaderTextureSet**: Texture file paths for materials

The method creates a new property block, adds it to the NIF file, and links it to the parent block's Properties array. Properties are processed in order, so the order matters for rendering.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The type of property block to create (e.g., "BSLightingShaderProperty") |

## Returns

Returns the newly created property block.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  shader: TwbNifBlock;
  texSet: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\clutter\common\bucket01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Add a lighting shader property
      shader := geometry.AddProperty('BSLightingShaderProperty');
      shader.NativeValues['Shader Flags 1'] := 2147483649; // Basic flags
      shader.NativeValues['Shader Flags 2'] := 1; // Enable textures

      // Add texture set
      texSet := shader.AddProperty('BSShaderTextureSet');
      texSet.EditValues['Textures\[0]'] := 'textures\clutter\bucket01_d.dds';
      texSet.EditValues['Textures\[1]'] := 'textures\clutter\bucket01_n.dds';

      AddMessage('Added shader property to geometry');
      nif.SaveToFile('meshes\clutter\common\bucket01_modified.nif');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_PropertyByName](TwbNifBlock_PropertyByName.md)
- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [TwbNifBlock_AddChild](TwbNifBlock_AddChild.md)
- [TwbNifBlock_AddExtraData](TwbNifBlock_AddExtraData.md)
