# ResourceContainerList

## Syntax

```pascal
procedure ResourceContainerList(AContainerNames: TStrings);
```

## Description

Appends the name of each loaded resource container to `AContainerNames`. It does not clear the list first. A BSA or BA2 contributes the archive path. A loose data folder contributes that folder path. A nil list is ignored.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerNames | TStrings | List that receives container names. Existing entries are kept |

## Returns

This procedure does not return a value.

## Example

```pascal
var
  containers: TStringList;
  i: Integer;
begin
  containers := TStringList.Create;
  try
    ResourceContainerList(containers);
    for i := 0 to Pred(containers.Count) do
      AddMessage(containers[i]);
  finally
    containers.Free;
  end;
end;
```

## See Also

- [ResourceList](IwbResource_ResourceList.md)
- [ResourceCount](IwbResource_ResourceCount.md)
