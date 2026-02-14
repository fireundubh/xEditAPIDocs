# OverrideCount (IwbMainRecord)

## Syntax

```pascal
function OverrideCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the number of overriding records for `ARecord`

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

- [AdditionalElementCount - IwbContainer](IwbContainer_AdditionalElementCount.md)
- [ElementCount - IwbElement](IwbContainer_ElementCount.md)
- [FileCount](Global_FileCount.md)
- [MasterCount - IwbFile](IwbFile_MasterCount.md)
- [OverrideByIndex - IwbMainRecord](IwbMainRecord_OverrideByIndex.md)
- [RecordCount - IwbFile](IwbFile_RecordCount.md)
- [ReferencedByCount - IwbMainRecord](IwbMainRecord_ReferencedByCount.md)
- [ReferencesCount - IwbMainRecord](IwbMainRecord_ReferencesCount.md)


