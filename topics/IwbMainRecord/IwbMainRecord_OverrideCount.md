# Syntax

```pascal
function OverrideCount(ARecord: IwbMainRecord): integer;
```

# Description

Returns the number of overriding records for `ARecord`

# Example

```pascal
for i := 0 to Pred(OverrideCount(e)) do
	o := OverrideByIndex(e, i);
```

# See Also

- [AdditionalElementCount - IwbContainer](IwbContainer/AdditionalElementCount)
- [ElementCount - IwbElement](IwbContainer/ElementCount)
- [FileCount](FileCount)
- [MasterCount - IwbFile](IwbFile/MasterCount)
- [OverrideByIndex - IwbMainRecord](IwbMainRecord/OverrideByIndex)
- [RecordCount - IwbFile](IwbFile/RecordCount)
- [ReferencedByCount - IwbMainRecord](IwbMainRecord/ReferencedByCount)
- [ReferencesCount - IwbMainRecord](IwbMainRecord/ReferencesCount)
