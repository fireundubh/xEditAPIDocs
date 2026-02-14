# ChildGroup

## Syntax

```pascal
function ChildGroup(AWorldspace: IwbMainRecord): IwbGroupRecord;
```

## Description

Returns the group contained by `AWorldspace`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AWorldspace | IwbMainRecord | The worldspace or other main record to get the child group from |

## Returns

Returns the IwbGroupRecord contained by the main record.

## Example

```pascal
grup := ChildGroup(wrld);
for i := 0 to Pred(ElementCount(grup)) do
	cell := ElementByIndex(grup, i);
```

## See Also

- [ChildrenOf](IwbGroupRecord_ChildrenOf.md)
- [FindChildGroup](IwbGroupRecord_FindChildGroup.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)
- [GroupLabel](IwbGroupRecord_GroupLabel.md)
- [GroupType](IwbGroupRecord_GroupType.md)


