# GroupBySignature

## Syntax

```pascal
function GroupBySignature(AFile: IwbFile; ASignature: String): IwbGroupRecord;
```

## Description

Returns the top-level group in `AFile` whose signature matches `ASignature`

## Example

```pascal
f := FileByIndex(0);  // IwbFile
g := GroupBySignature(f, 'ARMO');  // IwbGroupRecord
for i := 0 to Pred(ElementCount(g)) do
  r := ElementByIndex(g, i);  // IwbMainRecord
```

