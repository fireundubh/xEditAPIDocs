# ConflictThisForMainRecord

## Syntax

```pascal
function ConflictThisForMainRecord(aeRecord: IwbMainRecord): TConflictThis;
```

## Description

Gets the conflict status for a specific main record instance.

Returns a `TConflictThis` enumerated value indicating how this specific instance of the record relates to other versions of the same record in the load order.

## Example

```pascal
var
  record: IwbMainRecord;
  conflict: TConflictThis;
begin
  record := // ... get record reference
  conflict := ConflictThisForMainRecord(record);
  if conflict = ctMaster then
    AddMessage('This is the master record');
end;
```

## See Also

- [IwbMainRecord - Interface](Interface_IwbMainRecord.md)
- [TConflictThis - Enum](Enum_TConflictThis.md)
