# ResourceCount

## Syntax

```pascal
function ResourceCount(AFileName: String; AContainerNames: TStrings): Cardinal;
```

## Description

Populates `AContainers` list with the names of loaded resources that contain files matching `AFileName` and returns the match count

## Example

```pascal
slResList := TStringList.Create;
ResourceCount(aFileName, slResList);

for i := 0 to Pred(slResList.Count) do
  sContainerName := ExtractFileName(slResList[i]);
```
