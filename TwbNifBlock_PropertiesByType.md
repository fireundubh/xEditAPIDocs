# PropertiesByType

## Syntax

```pascal
procedure PropertiesByType(ABlockType: string; AList: TList);
procedure PropertiesByType(ABlockType: string; AList: TList; AInherited: Boolean);
```

**Access via:** `block.PropertiesByType(ABlockType, AList)` or `block.PropertiesByType(ABlockType, AList, Inherited)`

## Description

Populates a TList with all property blocks of a specific type attached to this block. Properties control rendering, materials, and visual characteristics.

The method can search for exact type matches or include inheritance. When inheritance checking is enabled, it includes all properties that are of the specified type or inherit from it.

Common property types to search for:
- "BSLightingShaderProperty" - Standard Skyrim/FO4 materials
- "BSEffectShaderProperty" - Special effect materials
- "NiAlphaProperty" - Alpha blending settings
- "NiMaterialProperty" - Material colors (older games)
- "BSShaderProperty" - Base shader class (with inheritance)

The list must be created before calling this method and should be freed by the caller.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlockType | string | The property type to search for |
| AList | TList | The list to populate with matching properties |
| AInherited | Boolean | Optional. If True, include inherited types; if False, exact match only. Default is False |

## Returns

This is a procedure (no return value). Results are added to the provided list.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  shaderList: TList;
  i: Integer;
  shader: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  shaderList := TList.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Find all shader properties (including derived types)
      geometry.PropertiesByType('BSShaderProperty', shaderList, True);

      AddMessage('Found ' + IntToStr(shaderList.Count) + ' shader properties:');
      for i := 0 to shaderList.Count - 1 do begin
        shader := TwbNifBlock(shaderList[i]);
        AddMessage('  ' + shader.BlockType);
      end;
    end;
  finally
    shaderList.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [TwbNifBlock_PropertyByName](TwbNifBlock_PropertyByName.md)
- [TwbNifBlock_ChildrenByType](TwbNifBlock_ChildrenByType.md)
- [TwbNifBlock_AddProperty](TwbNifBlock_AddProperty.md)
