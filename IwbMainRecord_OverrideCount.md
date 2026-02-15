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
// Example 1: Iterate through all overrides of a record
var
  overrideRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    count := OverrideCount(e);
    AddMessage(Format('%s has %d override(s):', [EditorID(e), count]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(e, i);
      if Assigned(overrideRec) then
        AddMessage(Format('  [%d] %s', [i, GetFileName(GetFile(overrideRec))]));
    end;
  end;
end;

// Example 2: Find records with most overrides
var
  plugin: IwbFile;
  rec, masterRec: IwbMainRecord;
  i, j, recCount, overrideCount, maxOverrides: integer;
  mostOverridden: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    recCount := RecordCount(plugin);
    maxOverrides := 0;

    for i := 0 to recCount - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and IsMaster(rec) then begin
        overrideCount := OverrideCount(rec);
        if overrideCount > maxOverrides then begin
          maxOverrides := overrideCount;
          mostOverridden := rec;
        end;
      end;
    end;

    if Assigned(mostOverridden) then
      AddMessage(Format('Most overridden: %s with %d overrides',
        [EditorID(mostOverridden), maxOverrides]));
  end;
end;

// Example 3: Check if record has any overrides before processing
var
  overrideRec: IwbMainRecord;
  count: integer;
begin
  if Assigned(e) then begin
    count := OverrideCount(e);

    if count = 0 then
      AddMessage(Format('%s: No overrides - safe to edit', [EditorID(e)]))
    else begin
      AddMessage(Format('%s: Has %d override(s) - check winning version',
        [EditorID(e), count]));

      overrideRec := WinningOverride(e);
      if Assigned(overrideRec) then
        AddMessage(Format('  Winning version in: %s',
          [GetFileName(GetFile(overrideRec))]));
    end;
  end;
end;

// Example 4: Copy field to all overrides
var
  overrideRec: IwbMainRecord;
  i, count: integer;
  newValue: string;
begin
  if Assigned(e) then begin
    newValue := 'Updated Description';
    count := OverrideCount(e);

    AddMessage(Format('Updating %d override(s)...', [count]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(e, i);
      if Assigned(overrideRec) then begin
        SetElementEditValue(overrideRec, 'DESC', newValue);
        AddMessage(Format('  Updated: %s', [GetFileName(GetFile(overrideRec))]));
      end;
    end;
  end;
end;
```

## See Also

- [OverrideByIndex - IwbMainRecord](IwbMainRecord_OverrideByIndex.md)
- [Master](IwbMainRecord_Master.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


