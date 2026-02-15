# TwbBGSMFile.Create

## Syntax

```pascal
function TwbBGSMFile.Create: TwbBGSMFile;
```

## Description

Creates a new BGSM (Bethesda Material) file handler instance.

BGSM is Bethesda's binary material format introduced in Fallout 4 and used in Fallout 76. It defines material properties for 3D models including texture paths, shader parameters, opacity, specularity, and other rendering properties. BGSM files replace the older NIF-embedded material system used in earlier games.

The created instance inherits from `TdfElement`, providing access to all data format manipulation methods for reading, modifying, and writing BGSM files. After creation, use `LoadFromFile` to read an existing BGSM, or populate the element tree manually to create a new material definition.

## Parameters

This function takes no parameters.

## Returns

Returns a new `TwbBGSMFile` instance ready for loading or creating BGSM material data.

## Example

```pascal
var
  bgsmFile: TwbBGSMFile;
begin
  // Create new BGSM handler
  bgsmFile := TwbBGSMFile.Create;
  try
    // Load existing material file
    bgsmFile.LoadFromFile('Textures\Materials\MyMaterial.bgsm');

    // Access material properties through TdfElement methods
    AddMessage('Diffuse texture: ' + bgsmFile.ElementByName('Diffuse Texture', True).EditValue);

    // Modify and save
    bgsmFile.ElementByName('Glossiness', True).EditValue := '0.5';
    bgsmFile.SaveToFile('Textures\Materials\MyMaterial_Modified.bgsm');
  finally
    bgsmFile.Free;
  end;
end;
```

## See Also

- [TwbBGEMFile.Create](TwbBGEMFile_Create.md) - Effect material format
- [TdfElement_LoadFromFile](TdfElement_LoadFromFile.md)
- [TdfElement_SaveToFile](TdfElement_SaveToFile.md)
- [TdfElement_ElementByName](TdfElement_ElementByName.md)
