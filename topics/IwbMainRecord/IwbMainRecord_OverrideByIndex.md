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

- [ElementByIndex - IwbContainer](IwbContainer_ElementByIndex.md)
- [FileByIndex](Global_FileByIndex.md)
- [OverrideCount - IwbMainRecord](IwbMainRecord_OverrideCount.md)
- [MasterByIndex - IwbFile](IwbFile_MasterByIndex.md)
- [RecordByIndex - IwbFile](IwbFile_RecordByIndex.md)
- [ReferencedByIndex - IwbMainRecord](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesByIndex - IwbMainRecord](IwbMainRecord_ReferencesByIndex.md)
