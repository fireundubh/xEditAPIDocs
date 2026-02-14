# GroupBySignature

## Syntax

```pascal
function GroupBySignature(AFile: IwbFile; ASignature: String): IwbGroupRecord;
```

## Description

Returns the top-level group in `AFile` whose signature matches `ASignature`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search for the group |
| ASignature | String | The 4-character signature of the group to find |

## Returns

Returns the group record with the specified signature as an IwbGroupRecord interface.

## Example

```pascal
f := FileByIndex(0);  // IwbFile
g := GroupBySignature(f, 'ARMO');  // IwbGroupRecord
for i := 0 to Pred(ElementCount(g)) do
  r := ElementByIndex(g, i);  // IwbMainRecord
```

