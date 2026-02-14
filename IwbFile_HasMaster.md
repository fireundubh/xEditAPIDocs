# HasMaster

## Syntax

```pascal
function HasMaster(AFile: IwbFile; AFileName: String): Boolean;
```

## Description

Returns `True` if `AFile` depends on a master file named `AFileName`, and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check for master dependencies |
| AFileName | String | The name of the master file to look for |

## Returns

Returns `True` if `AFile` depends on a master file named `AFileName`, and `False` otherwise.

## Example

```pascal
f := FileByName('Dawnguard.esm');
if HasMaster(f, 'Skyrim.esm') then
  AddMessage('Dawnguard.esm depends on Skyrim.esm');
```

