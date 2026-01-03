# GetIsESL

## Syntax

```pascal
function GetIsESL(AFile: IwbFile): Boolean;
```

## Description

Returns `True` if `AFile` is an ESL plugin, and `False` otherwise

## Example

```pascal
if GetIsESL(f) then
	AddMessage(GetFileName(f) + ' is an ESL!');
```

