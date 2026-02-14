# ReferencedByCount

## Syntax

```pascal
function ReferencedByCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the count of records that reference this record via FormID fields.

This function retrieves the ReferencedByCount property, which counts all records containing FormID fields that point to this record. This includes all reference types (base object references, parent references, etc.). Returns 0 for unreferenced records or invalid inputs. Building the reference list may be slow for heavily-referenced records. Use BuildRef first to ensure references are tracked.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to count incoming references for |

## Returns

Returns the number of records that reference this record as an integer.

## Example

```pascal
for i := 0 to Pred(ReferencedByCount(e)) do
	r := ReferencedByIndex(e, i);
```

## See Also

- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [BuildRef](IwbElement_BuildRef.md)
- [LinksTo](IwbElement_LinksTo.md)


