# ConflictAllForMainRecord

## Syntax

```pascal
function ConflictAllForMainRecord(aeRecord: IwbMainRecord): TConflictAll;
```

## Description

Gets the overall conflict status for a main record across all plugins.

Returns a `TConflictAll` enumerated value indicating how this record conflicts with its counterparts in other plugins that modify it.

## Example

```pascal
var
  record: IwbMainRecord;
  conflict: TConflictAll;
begin
  record := // ... get record reference
  conflict := ConflictAllForMainRecord(record);
  if conflict = caOverride then
    AddMessage('Record is overridden');
end;
```
