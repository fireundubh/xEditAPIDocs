# ResourceOpenData

## Syntax

```pascal
function ResourceOpenData(AContainerName: string; AFileName: string): TBytes;
```

## Description

Loads the resource matching `AFileName`, iterates through that resource until matching on a container named `AContainerName`, and returns its data as a byte array

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainerName | string | The name of the container to search within (empty string for any container) |
| AFileName | string | The name of the file to load from the resource |

## Returns

Returns the file data as a TBytes array.

## Example

```pascal
NifTextureList(ResourceOpenData('', 'meshes\' + mesh), slTex);
```

