# ResourceExists

## Syntax

```pascal
function ResourceExists(AFileName: string): Boolean;
```

## Description

Returns True when any loaded container has `AFileName`. The path is the name inside a BSA or BA2, or the path under a loose data folder. The search stops at the first container that has the file.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFileName | string | Resource path to look for |

## Returns

True if a loaded container has the file, otherwise False.

## Example

```pascal
var
  fileName: string;
begin
  fileName := 'meshes\clutter\bucket01.nif';
  if ResourceExists(fileName) then
    AddMessage(fileName + ' is in a loaded container');
end;
```

## See Also

- [ResourceCount](IwbResource_ResourceCount.md)
- [ResourceOpenData](IwbResource_ResourceOpenData.md)
