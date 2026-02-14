# NifTextureList

## Syntax

```pascal
function NifTextureList(aData: TBytes; aList: TStrings): Boolean;
```

## Description

Extracts all texture file paths referenced by a NIF (NetImmerse File Format) mesh file and adds them to a string list. This function parses the NIF binary structure and identifies all texture resources used by the mesh.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aData | TBytes | The raw binary data of the NIF file |
| aList | TStrings | The string list to receive the texture paths |

## Returns

Returns True if the NIF was successfully parsed and texture paths were extracted, False otherwise.

## Example

```pascal
var
  nifData: TBytes;
  textureList: TStringList;
begin
  textureList := TStringList.Create;
  try
    nifData := ResourceOpenData('', 'meshes\architecture\windhelm\whhousestone01.nif');

    if NifTextureList(nifData, textureList) then
      AddMessage('Mesh uses ' + IntToStr(textureList.Count) + ' textures');
  finally
    textureList.Free;
  end;
end;
```

## See Also

- [NifTextureListResource](IwbResource_NifTextureListResource.md)
- [NifTextureListUVRange](IwbResource_NifTextureListUVRange.md)
- [NifBlockList](IwbResource_NifBlockList.md)
