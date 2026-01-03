# OverrideByIndex

## Syntax

```pascal
function OverrideByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the overriding record for `ARecord` at `AIndex` in the array of overriding records for that record

## Example

```pascal
for i := 0 to Pred(OverrideCount(e)) do
	o := OverrideByIndex(e, i);
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [FileByIndex](Global_FileByIndex.md)
- [OverrideCount](IwbMainRecord_OverrideCount.md)
- [MasterByIndex](IwbFile_MasterByIndex.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)


