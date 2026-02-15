# PropertyByType

## Syntax

```pascal
function PropertyByType(ABlock: TwbNifBlock; ABlockType: string): TwbNifBlock;
function PropertyByType(ABlock: TwbNifBlock; ABlockType: string; AInherited: Boolean): TwbNifBlock;
```

## Description

Finds and returns the first property block of a specific type attached to this block. Returns nil if no matching property is found.

This is a convenience method for finding a single property when you expect only one or only need the first match. It's commonly used to locate the shader property, alpha property, or other rendering properties attached to geometry.

The function supports both exact type matching and inheritance checking. When inheritance is enabled, it returns the first property that is of the specified type or inherits from it.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The block whose properties to search |
| ABlockType | string | The property type to search for |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

Returns the first matching property block, or nil if none found.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  shader: TwbNifBlock;
  texSet: TwbNifBlock;
  alphaProp: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\effects\fxambientdust01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Get the shader property
      shader := PropertyByType(geometry, 'BSLightingShaderProperty', False);

      if Assigned(shader) then begin
        AddMessage('Shader Flags 1: ' + IntToStr(shader.ElementByPath['Shader Flags 1'].NativeValue));

        // Many shaders have a texture set as a child property
        texSet := PropertyByType(shader, 'BSShaderTextureSet', False);
        if Assigned(texSet) then
          AddMessage('Diffuse: ' + texSet.ElementByPath['Textures\[0]'].EditValue);
      end;

      // Check for alpha property
      alphaProp := PropertyByType(geometry, 'NiAlphaProperty', False);
      if Assigned(alphaProp) then
        AddMessage('Has alpha blending');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_PropertiesByType](TwbNifBlock_PropertiesByType.md)
- [TwbNifBlock_PropertyByName](TwbNifBlock_PropertyByName.md)
- [TwbNifBlock_ChildByType](TwbNifBlock_ChildByType.md)
- [TwbNifBlock_AddProperty](TwbNifBlock_AddProperty.md)
