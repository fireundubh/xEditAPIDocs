# GroupBySignature

## Syntax

```pascal
function GroupBySignature(AFile: IwbFile; ASignature: string): IwbGroupRecord;
```

## Description

Returns the top-level group in `AFile` whose signature is `ASignature`.

`ASignature` must be at least four characters. A shorter string raises. Only the first four characters are used.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search |
| ASignature | string | Four-character record signature, such as `ARMO` |

## Returns

The top-level group, or nil when `AFile` has no such group. If `AFile` is not a file, the result is unassigned.

## Example

```pascal
var
  f: IwbFile;
  g: IwbGroupRecord;
  rec: IwbElement;
  i: Integer;
begin
  f := FileByIndex(0);
  if Assigned(f) then begin
    g := GroupBySignature(f, 'ARMO');
    if Assigned(g) then
      for i := 0 to Pred(ElementCount(g)) do begin
        rec := ElementByIndex(g, i);
        if Assigned(rec) then
          AddMessage(Name(rec));
      end;
  end;
end;
```

## See Also

- [HasGroup](IwbFile_HasGroup.md)
- [ElementCount](IwbContainer_ElementCount.md)
- [ElementByIndex](IwbContainer_ElementByIndex.md)
