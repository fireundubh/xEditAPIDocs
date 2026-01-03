# ReferencesCount

## Syntax

```pascal
function ReferencesCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the number of records linked to by `ARecord`

## Example

```pascal
for i := 0 to Pred(ReferencesCount(e)) do
	r := ReferencesByIndex(e, i);
```

## See Also

- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)


