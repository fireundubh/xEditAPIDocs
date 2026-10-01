# ResourceCount

## Syntax

```pascal
function ResourceCount(AFileName: string; AContainers: TStrings): Integer;
```

## Description

Counts loaded containers that contain `AFileName`. Each match is appended to `AContainers`. The list is not cleared first. The order is the container load order.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | Resource path to look for, such as `meshes\clutter\bucket01.nif` |
| AContainers | TStrings | List that receives the name of each container that has the file |

## Returns

The number of matching containers.

## Example

```pascal
var
  containers: TStringList;
  fileName: string;
  n, i: Integer;
begin
  fileName := 'meshes\clutter\bucket01.nif';
  containers := TStringList.Create;
  try
    n := ResourceCount(fileName, containers);
    AddMessage(fileName + ' is in ' + IntToStr(n) + ' containers');
    for i := 0 to Pred(containers.Count) do
      AddMessage(containers[i]);
  finally
    containers.Free;
  end;
end;
```

## See Also

- [ResourceExists](IwbResource_ResourceExists.md)
- [ResourceContainerList](IwbResource_ResourceContainerList.md)
- [ResourceCopy](IwbResource_ResourceCopy.md)
