# HasMaster

## Syntax

```pascal
function HasMaster(AFile: IwbFile; AFileName: String): Boolean;
```

## Description

Returns `True` if `AFile` depends on a master file named `AFileName`, and `False` otherwise

## Example

```pascal
f := FileByName('Dawnguard.esm');
if HasMaster(f, 'Skyrim.esm') then
  AddMessage('Dawnguard.esm depends on Skyrim.esm');
```
