# CanBeESL

## Syntax

```pascal
function CanBeESL(AFile: IwbFile): Boolean;
```

## Description

Returns whether `AFile` can be an ESL (Light) file.

## Example

```pascal
if CanBeESL(f) then
  SetIsESL(f, True);
```

## See Also

- [CanBeLight](IwbFile_CanBeLight.md)
- [GetIsESL](IwbFile_GetIsESL.md)
- [SetIsESL](IwbFile_SetIsESL.md)
