# NifTextureList

## Syntax

```pascal
function NifTextureList(AData: TBytes; AList: TStrings): Boolean;
```

## Description

Clears `AList` and fills it with texture paths from BSShaderTextureSet and BSEffectShaderProperty blocks. Empty paths are removed. A nil list or an empty `AData` returns False. A NIF that loads returns True even when it has no textures.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AData | TBytes | The raw binary data of the NIF file |
| AList | TStrings | The string list to receive the texture paths |

## Returns

True when the NIF loaded. False when `AList` is nil, `AData` is empty, or the NIF did not load.

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
