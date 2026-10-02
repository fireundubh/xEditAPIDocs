# TwbBGEMFile.Create

## Syntax

```pascal
function TwbBGEMFile.Create: TwbBGEMFile;
```

## Description

Creates a new BGEM (Bethesda Effect Material) file handler instance.

BGEM is Bethesda's binary format for effect materials introduced in Fallout 4 and used in Fallout 76. It defines material properties for particle effects, magic effects, and other special visual effects. BGEM files specify texture paths, blend modes, particle properties, and shader parameters for rendering visual effects.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading, modifying, and writing BGEM files. After creation, use `LoadFromFile` to read an existing BGEM, or populate the element tree manually to create a new effect material definition.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbBGEMFile` instance ready for loading or creating BGEM effect material data.

## Example

```pascal
var
  bgemFile: TwbBGEMFile;
begin
  bgemFile := TwbBGEMFile.Create;
  try
    bgemFile.LoadFromFile('materials\MyEffect.bgem');

    AddMessage('Base texture: ' + bgemFile.EditValues['Textures\Base']);

    bgemFile.EditValues['AlphaBlendMode'] := 'Additive';
    bgemFile.SaveToFile('materials\MyEffect_Modified.bgem');
  finally
    bgemFile.Free;
  end;
end;
```

## See Also

- [TwbBGSMFile.Create](TwbBGSMFile_Create.md) - Standard material format
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement_ElementByName](TdfElement_ElementByName.md)
