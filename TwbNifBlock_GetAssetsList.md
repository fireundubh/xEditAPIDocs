# GetAssetsList

## Syntax

```pascal
function GetAssetsList(ABlock: TwbNifBlock): string;
procedure GetAssetsList(ABlock: TwbNifBlock; AList: TStrings);
```

## Description

Retrieves the list of asset file paths referenced by this block and its children. Assets include textures, material files, and other external resources.

When called with no parameters, returns a newline-delimited string of asset paths. When called with a TStrings parameter, adds each asset path to the provided list.

This function searches the block and all its child blocks for asset references including:
- Texture file paths (diffuse, normal, specular, etc.)
- Material files (BGSM, BGEM)
- Other referenced files

Asset paths are typically relative to the game's Data folder.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ABlock | TwbNifBlock | The block to search for asset references |
| AList | TStrings | Optional. If provided, assets are added to this list |

## Returns

When called without parameters, returns a string with asset paths separated by newlines. When called with a TStrings parameter, returns nothing (procedure).

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  assets: TStringList;
  i: Integer;
  assetStr: string;
begin
  nif := TwbNifFile.Create;
  assets := TStringList.Create;
  try
    nif.LoadFromFile('meshes\architecture\windhelm\whbuilding01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      // Get assets as a delimited string
      assetStr := GetAssetsList(geometry);
      AddMessage('Assets (string): ' + assetStr);

      // Get assets in a list for easier processing
      GetAssetsList(geometry, assets);
      AddMessage('Found ' + IntToStr(assets.Count) + ' assets:');
      for i := 0 to assets.Count - 1 do
        AddMessage('  ' + assets[i]);
    end;
  finally
    assets.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifFile_GetAssetsList](TwbNifFile_GetAssetsList.md)
- [TwbNifBlock_PropertyByType](TwbNifBlock_PropertyByType.md)
- [IwbResource_NifTextureList](IwbResource_NifTextureList.md)
