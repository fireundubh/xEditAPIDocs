# ChildGroup

## Syntax

```pascal
function ChildGroup(AWorldspace: IwbMainRecord): IwbGroupRecord;
```

## Description

Returns the group contained by `AWorldspace`

## Example

```pascal
grup := ChildGroup(wrld);
for i := 0 to Pred(ElementCount(grup)) do
	cell := ElementByIndex(grup, i);
```

## See Also

- [ChildrenOf](../IwbGroupRecord/IwbGroupRecord_ChildrenOf.md)
- [FindChildGroup](../IwbGroupRecord/IwbGroupRecord_FindChildGroup.md)
- [GroupBySignature](../IwbFile/IwbFile_GroupBySignature.md)
- [GroupLabel](../IwbGroupRecord/IwbGroupRecord_GroupLabel.md)
- [GroupType](../IwbGroupRecord/IwbGroupRecord_GroupType.md)
