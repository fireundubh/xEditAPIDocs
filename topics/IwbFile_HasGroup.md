# HasGroup

## Syntax

```pascal
function HasGroup(AFile: IwbFile; ASignature: String): Boolean;
```

## Description

Returns `True` if a top-level group whose signature matches `ASignature` exists in `AFile`, and `False` otherwise

## Example

```pascal
f := FileByIndex(0);
if HasGroup(f, 'ARMO') then
  AddMessage('Skyrim.esm has top-level group: ARMO');
```

