# HasGroup

## Syntax

```pascal
function HasGroup(AFile: IwbFile; ASignature: String): Boolean;
```

## Description

Returns `True` if a top-level group whose signature matches `ASignature` exists in `AFile`, and `False` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search for the group |
| ASignature | String | The signature of the group to find |

## Returns

Returns `True` if the group exists, `False` otherwise.

## Example

```pascal
f := FileByIndex(0);
if HasGroup(f, 'ARMO') then
  AddMessage('Skyrim.esm has top-level group: ARMO');
```

