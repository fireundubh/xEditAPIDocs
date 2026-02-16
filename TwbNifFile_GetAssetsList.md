# GetAssetsList

## Syntax

```pascal
function GetAssetsList: string;
procedure GetAssetsList(AList: TStrings);
```

Access via: `nifFile.GetAssetsList` or `nifFile.GetAssetsList(List)`

## Description

Retrieves a comprehensive list of all asset file paths referenced by the NIF file. Assets include textures, material files, and other external resources referenced by blocks throughout the file.

When called with no parameters, returns a newline-delimited string of asset paths. When called with a TStrings parameter, adds each asset path to the provided list.

This function searches all blocks in the file for asset references including:
- Texture file paths from shader properties and texture sets
- Material files (BGSM, BGEM) referenced by shaders
- Other external resource references
- Duplicate paths are included if referenced multiple times

Asset paths are typically relative to the game's Data folder and use backslash separators.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList | TStrings | Optional. If provided, assets are added to this list |

## Returns

When called without parameters, returns a string with asset paths separated by newlines. When called with a TStrings parameter, returns nothing (procedure).

## Example

```pascal
var
  nif: TwbNifFile;
  assets: TStringList;
  i: Integer;
  uniqueAssets: TStringList;
begin
  nif := TwbNifFile.Create;
  assets := TStringList.Create;
  uniqueAssets := TStringList.Create;
  try
    nif.LoadFromFile('meshes\architecture\whiterun\wrterrain01.nif');

    // Get all assets
    nif.GetAssetsList(assets);

    AddMessage('Total asset references: ' + IntToStr(assets.Count));

    // Remove duplicates
    uniqueAssets.Duplicates := dupIgnore;
    uniqueAssets.Sorted := True;
    for i := 0 to assets.Count - 1 do
      uniqueAssets.Add(assets[i]);

    AddMessage('Unique assets: ' + IntToStr(uniqueAssets.Count));

    // List all unique assets
    for i := 0 to uniqueAssets.Count - 1 do
      AddMessage('  ' + uniqueAssets[i]);
  finally
    uniqueAssets.Free;
    assets.Free;
    nif.Free;
  end;
end;
```

## Example (Verify Asset Existence)

```pascal
var
  nif: TwbNifFile;
  assets: TStringList;
  i: Integer;
  assetPath: string;
  missingCount: Integer;
begin
  nif := TwbNifFile.Create;
  assets := TStringList.Create;
  try
    nif.LoadFromFile('meshes\armor\iron\ironarmor.nif');
    nif.GetAssetsList(assets);

    missingCount := 0;

    for i := 0 to assets.Count - 1 do begin
      assetPath := assets[i];

      if not ResourceExists(assetPath) then begin
        AddMessage('Missing: ' + assetPath);
        Inc(missingCount);
      end;
    end;

    if missingCount = 0 then
      AddMessage('All assets exist')
    else
      AddMessage('Missing ' + IntToStr(missingCount) + ' assets');
  finally
    assets.Free;
    nif.Free;
  end;
end;
```

## See Also

- [TwbNifBlock_GetAssetsList](TwbNifBlock_GetAssetsList.md)
- [IwbResource_NifTextureList](IwbResource_NifTextureList.md)
- [IwbResource_NifTextureListResource](IwbResource_NifTextureListResource.md)
