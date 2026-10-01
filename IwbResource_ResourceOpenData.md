# ResourceOpenData

## Syntax

```pascal
function ResourceOpenData(AContainerName: string; AFileName: string): TBytes;
```

## Description

Reads one resource and returns its bytes. The search is by `AFileName` across loaded containers, from the last container back to the first. An empty `AContainerName` accepts the first hit in that order, which is the last loaded container that has the file. A non-empty name accepts the first hit whose container name matches, ignoring letter case.

A missing file returns an empty array. It does not raise.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | Container name, or `''` for the last loaded match |
| AFileName | string | Resource path inside the container, such as `meshes\clutter\bucket01.nif` |

## Returns

The file bytes, or an empty `TBytes` when no container has that file.

## Example

```pascal
var
  data: TBytes;
begin
  data := ResourceOpenData('', 'meshes\clutter\bucket01.nif');
  if Length(data) > 0 then
    AddMessage('Bucket mesh is ' + IntToStr(Length(data)) + ' bytes');
end;
```

## See Also

- [ResourceExists](IwbResource_ResourceExists.md)
- [ResourceCopy](IwbResource_ResourceCopy.md)
- [wbCRC32Resource](IwbResource_wbCRC32Resource.md)
