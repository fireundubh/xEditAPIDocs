# ConflictThisForMainRecord

## Syntax

```pascal
function ConflictThisForMainRecord(aeRecord: IwbMainRecord): TConflictThis;
```

## Description

Gets the conflict status for a specific main record instance.

Returns a `TConflictThis` enumerated value indicating how this specific instance of the record relates to other versions of the same record in the load order.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aeRecord | IwbMainRecord | The main record to get the specific conflict status for |

## Returns

Returns a TConflictThis enumeration value indicating the specific conflict status.

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

