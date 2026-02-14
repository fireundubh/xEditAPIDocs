# OverrideCount (IwbMainRecord)

## Syntax

```pascal
function OverrideCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the total number of records overriding this record.

This function retrieves the OverrideCount property, which counts all records in lower-priority files that modify the same FormID. Returns 0 for records with no overrides or invalid inputs. Use with OverrideByIndex to iterate through all overrides. The count includes all overrides regardless of load order, but the master record must have been loaded first.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The master record to count overrides for |

## Returns

Returns the number of overriding records as an integer.

## Example

```pascal
for i := 0 to Pred(OverrideCount(e)) do
	o := OverrideByIndex(e, i);
```

## See Also

- [OverrideByIndex - IwbMainRecord](IwbMainRecord_OverrideByIndex.md)
- [Master](IwbMainRecord_Master.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


