# OverrideByIndex

## Syntax

```pascal
function OverrideByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the override record at the specified index in the override list.

This function accesses the Overrides property by index, providing array-style access to all records overriding this record. Overrides are ordered by load order (lowest to highest). Index 0 is the first override, not the master. Use OverrideCount to get the valid index range. Returns nil for invalid indices. Useful for iterating through the entire override chain.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The master record to get the override from |
| AIndex | integer | The zero-based index of the override in the override list |

## Returns

Returns the IwbMainRecord override at the specified index.

## Example

```pascal
for i := 0 to Pred(OverrideCount(e)) do
	o := OverrideByIndex(e, i);
```

## See Also

- [OverrideCount](IwbMainRecord_OverrideCount.md)
- [Master](IwbMainRecord_Master.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


