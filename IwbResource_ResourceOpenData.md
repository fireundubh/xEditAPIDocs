# ResourceOpenData

## Syntax

```pascal
function ResourceOpenData(AContainerName: string; AFileName: string): TBytes;
```

## Description

Loads the resource matching `AFileName`, iterates through that resource until matching on a container named `AContainerName`, and returns its data as a byte array

## Example

```pascal
NifTextureList(ResourceOpenData('', 'meshes\' + mesh), slTex);
```

