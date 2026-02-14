# GetIsESM

## Syntax

```pascal
function GetIsESM(AFile: IwbFile): Boolean;
```

## Description

Returns `True` if `AFile` is an ESM plugin, and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it's an ESM |

## Returns

Returns true if the file is an ESM plugin, false otherwise.

## Example

```pascal
if GetIsESM(f) then
  AddMessage(GetFileName(f) + ' is an ESM!');
```

