# NifTextureListResource

## Syntax

```pascal
function NifTextureListResource(aContainerName: string; aResourceName: string; aList: TStrings): Boolean;
```

## Description

Extracts all texture file paths from a NIF mesh file stored in a BSA or BA2 archive and adds them to a string list. This is a convenience wrapper that opens the resource data and calls NifTextureList internally.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aContainerName | string | The name of the BSA/BA2 archive containing the mesh (empty string searches all) |
| aResourceName | string | The path to the NIF file within the archive |
| aList | TStrings | The string list to receive the texture paths |

## Returns

Returns True if the NIF was successfully loaded and texture paths were extracted, False otherwise.

## Example

```pascal
var
  textureList: TStringList;
begin
  textureList := TStringList.Create;
  try
    if NifTextureListResource('', 'meshes\clutter\common\bucket01.nif', textureList) then
      AddMessage('Found ' + IntToStr(textureList.Count) + ' textures in bucket mesh');
  finally
    textureList.Free;
  end;
end;
```

## See Also

- [NifTextureList](IwbResource_NifTextureList.md)
- [NifTextureListUVRange](IwbResource_NifTextureListUVRange.md)
- [ResourceOpenData](IwbContainer_ResourceOpenData.md)
