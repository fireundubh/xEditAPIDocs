# ReferencesCount

## Syntax

```pascal
function ReferencesCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the number of records linked to by `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to count outgoing references for |

## Returns

Returns the number of records this record references as an integer.

## Example

```pascal
for i := 0 to Pred(ReferencesCount(e)) do
	r := ReferencesByIndex(e, i);
```

## See Also

- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)
- [BuildRef](IwbElement_BuildRef.md)


