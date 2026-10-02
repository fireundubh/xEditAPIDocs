# GetAssetsList

## Syntax

```pascal
function GetAssetsList: Variant;
procedure GetAssetsList(AList: TStrings);
```

**Access via:** `block.GetAssetsList` or `block.GetAssetsList(AList)`

## Description

Registered on `TwbNifBlock`, but the block implementation returns no paths. The no-argument call does not produce asset paths. The `TStrings` call adds nothing and returns nothing.

Use [TwbNifFile.GetAssetsList](TwbNifFile_GetAssetsList.md) to list textures and other external files in the NIF.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AList | TStrings | Optional. When passed, the call appends to this list. The block implementation appends nothing |

## Returns

The no-argument call returns no asset paths. The `TStrings` call returns nothing.

## Example

```pascal
var
  nif: TwbNifFile;
  geometry: TwbNifBlock;
  assets: TStringList;
begin
  nif := TwbNifFile.Create;
  assets := TStringList.Create;
  try
    nif.LoadFromFile('meshes\architecture\windhelm\whbuilding01.nif');

    geometry := nif.BlockByType('BSTriShape');

    if Assigned(geometry) then begin
      geometry.GetAssetsList(assets);
      AddMessage('Block asset count: ' + IntToStr(assets.Count));
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
