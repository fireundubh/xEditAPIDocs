# ResourceList

## Syntax

```pascal
procedure ResourceList(AContainerName: string; AResourceNames: TStrings);
procedure ResourceList(AContainerName: string; AResourceNames: TStrings; AFolder: string);
```

## Description

Appends resource names to `AResourceNames`. It does not clear the list first.

An empty `AContainerName` walks every loaded container. A non-empty name stops at the first container whose name matches, ignoring letter case. Names are the paths stored in a BSA or BA2, or paths relative to a loose folder.

`AFolder` limits the list. For an archive it is a prefix of the resource name. For a loose folder it is a subdirectory, and names under that directory are included. Omit it, or pass `''`, to list the whole container. Names from a loose folder are lowercased. Names from an archive are the names stored in the archive. Zero or one argument is an error, and so is a fourth argument.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | Container name from [ResourceContainerList](IwbResource_ResourceContainerList.md). Empty lists every container |
| AResourceNames | TStrings | List that receives resource names. Existing entries are kept |
| AFolder | string | Optional folder prefix. Empty lists the whole container |

## Returns

This procedure does not return a value.

## Example

```pascal
var
  containers, assets: TStringList;
  i: Integer;
begin
  containers := TStringList.Create;
  assets := TStringList.Create;
  try
    ResourceContainerList(containers);
    for i := 0 to Pred(containers.Count) do
      ResourceList(containers[i], assets, 'meshes\clutter\');
    AddMessage('Clutter meshes: ' + IntToStr(assets.Count));
  finally
    assets.Free;
    containers.Free;
  end;
end;
```

## See Also

- [ResourceContainerList](IwbResource_ResourceContainerList.md)
- [ResourceExists](IwbResource_ResourceExists.md)
- [ResourceOpenData](IwbResource_ResourceOpenData.md)
