# NifTextureListResource

## Syntax

```pascal
function NifTextureListResource(AContainerName: string; AResourceName: string; AList: TStrings): Boolean;
```

## Description

Opens a NIF with [ResourceOpenData](IwbResource_ResourceOpenData.md) and passes the bytes to [NifTextureList](IwbResource_NifTextureList.md). An empty `AContainerName` uses the last loaded container that has the file. A missing file yields empty bytes, and [NifTextureList](IwbResource_NifTextureList.md) then returns False.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | Container name, or `''` for the last loaded match |
| AResourceName | string | The path to the NIF file within the archive |
| AList | TStrings | The string list to receive the texture paths |

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
- [ResourceOpenData](IwbResource_ResourceOpenData.md)
