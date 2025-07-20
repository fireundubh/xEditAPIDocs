# ResourceList

## Syntax

```pascal
procedure ResourceList(AContainerName: String; AContainerNames: TStrings);
```

## Description

Populates `AContainerNames` with all file names in the container matching `AContainerName`

## Example

```pascal
slContainers := TStringList.Create;
slAssets := TwbFastStringList.Create;
try
  ResourceContainerList(slContainers);
  for i := 0 to Pred(slContainers.Count) do
    ResourceList(slContainers[i], slAssets);  // <--
  slAssets.Sort;
  wbRemoveDuplicateStrings(slAssets);
  wbFilterStrings(slAssets, slCloudTextures, sCloudTexturesLocation);
finally
  slAssets.Free;
  slContainers.Free;
end;
```
