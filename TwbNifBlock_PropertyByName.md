# PropertyByName

## Syntax

```pascal
function PropertyByName(ABlock: TwbNifBlock; AName: string): TwbNifBlock;
```

## Description

Finds and returns a property block attached to this block by searching for a matching name. Returns nil if no property with the specified name is found.

Some property blocks have a Name field that can be used to identify specific properties. This is useful when multiple properties of different types are attached to a single block and you need to find a specific one by name.

Note that not all property types support names. This method is most useful for custom properties or when working with NIFs that use named properties for organization.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The block whose properties to search |
| AName | string | The name of the property to find |

## Returns

Returns the property block with the matching name, or nil if not found.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  namedProp: TwbNifBlock;
begin
  nif := TwbNifFile.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrcarpet01.nif');

    geometry := nif.BlockByType('NiTriShape');

    if Assigned(geometry) then begin
      // Try to find a property by name
      namedProp := PropertyByName(geometry, 'CustomMaterial');

      if Assigned(namedProp) then
        AddMessage('Found property: ' + BlockType(namedProp))
      else
        AddMessage('Property "CustomMaterial" not found');
    end;
  finally
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [TwbNifBlock_PropertiesByType](TwbNifBlock_PropertiesByType.md)
- [TwbNifBlock_ExtraDataByName](TwbNifBlock_ExtraDataByName.md)
- [TwbNifBlock_AddProperty](TwbNifBlock_AddProperty.md)
