# HasGroup

## Syntax

```pascal
function HasGroup(AFile: IwbFile; ASignature: string): Boolean;
```

## Description

Returns whether `AFile` has a top-level group with signature `ASignature`.

`ASignature` must be at least four characters. A shorter string raises. Only the first four characters are used.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search |
| ASignature | string | Four-character record signature, such as `ARMO` |

## Returns

`True` when the group exists, `False` when it does not. If `AFile` is not a file, the result is unassigned.

## Example

```pascal
var
  f: IwbFile;
begin
  f := FileByIndex(0);
  if Assigned(f) and HasGroup(f, 'ARMO') then
    AddMessage(GetFileName(f) + ' has an ARMO group');
end;
```

## See Also

- [GroupBySignature](IwbFile_GroupBySignature.md)
