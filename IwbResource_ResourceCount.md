# ResourceCount

## Syntax

```pascal
function ResourceCount(AFileName: String; AContainerNames: TStrings): Cardinal;
```

## Description

Populates `AContainers` list with the names of loaded resources that contain files matching `AFileName` and returns the match count

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | String | The file name to search for within resource containers |
| AContainerNames | TStrings | The string list to populate with matching container names |

## Returns

Returns the number of resource containers that contain the specified file.

## Example

```pascal
slResList := TStringList.Create;
ResourceCount(aFileName, slResList);

for i := 0 to Pred(slResList.Count) do
  sContainerName := ExtractFileName(slResList[i]);
```

