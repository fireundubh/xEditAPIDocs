# ResourceCopy

## Syntax

```pascal
procedure ResourceCopy(AContainerName: string; AFileName: string; APathOut: string);
```

## Description

Copies one resource to disk. Container selection matches [ResourceOpenData](IwbResource_ResourceOpenData.md): an empty `AContainerName` uses the last loaded container that has the file.

If `APathOut` has an extension, that path is the output file. If it does not, `AFileName` is appended as a relative path under that directory. Missing destination directories are created.

The call raises when `APathOut` is empty, when the resource is missing, or when the destination directory cannot be created.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | Container name, or `''` for the last loaded match |
| AFileName | string | Resource path inside the container |
| APathOut | string | Output file path, or a directory that receives `AFileName` |

## Returns

This procedure does not return a value.

## Example

```pascal
var
  containers: TStringList;
  fileName, dest: string;
begin
  fileName := 'meshes\clutter\bucket01.nif';
  containers := TStringList.Create;
  try
    if ResourceCount(fileName, containers) = 0 then
      Exit;
    dest := wbTempPath + 'bucket01.nif';
    ResourceCopy(containers[0], fileName, dest);
    AddMessage('Copied to ' + dest);
  finally
    containers.Free;
  end;
end;
```

## See Also

- [ResourceOpenData](IwbResource_ResourceOpenData.md)
- [ResourceCount](IwbResource_ResourceCount.md)
