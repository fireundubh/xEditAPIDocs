# ReferencedByCount

## Syntax

```pascal
function ReferencedByCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the number of records linking to `ARecord`

## Example

```pascal
for i := 0 to Pred(ReferencedByCount(e)) do
	r := ReferencedByIndex(e, i);
```

## See Also

- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
