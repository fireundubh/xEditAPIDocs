# GetIsESM

## Syntax

```pascal
function GetIsESM(AFile: IwbFile): Boolean;
```

## Description

Returns `True` if `AFile` is an ESM plugin, and `False` otherwise

## Example

```pascal
if GetIsESM(f) then
  AddMessage(GetFileName(f) + ' is an ESM!');
```

