# GetIsESL

## Syntax

```pascal
function GetIsESL(AFile: IwbFile): Boolean;
```

## Description

Returns `True` if `AFile` is an ESL plugin, and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to check if it's an ESL |

## Returns

Returns true if the file is an ESL plugin, false otherwise.

## Example

```pascal
if GetIsESL(f) then
	AddMessage(GetFileName(f) + ' is an ESL!');
```

