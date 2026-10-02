# ConflictAllForMainRecord

## Syntax

```pascal
function ConflictAllForMainRecord(ARecord: IwbMainRecord): integer;
```

## Description

Gets the overall conflict status for a main record across all plugins.

Returns one of the `ca*` constants (`caUnknown` through `caConflictCritical`), indicating how this record conflicts with its counterparts in other plugins that modify it. Passing a value that is not a main record raises an error.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the overall conflict status for |

## Returns

Returns the integer value of a `ca*` constant. Raises an error when `ARecord` is not a main record.

## Example

```pascal
// Example 1: Check overall conflict status
var
  conflictAll: integer;
  conflictStr: string;
begin
  if Assigned(e) then begin
    conflictAll := ConflictAllForMainRecord(e);

    case conflictAll of
      caUnknown: conflictStr := 'Unknown';
      caOnlyOne: conflictStr := 'Only One';
      caNoConflict: conflictStr := 'No Conflict';
      caConflictBenign: conflictStr := 'Benign Conflict';
      caOverride: conflictStr := 'Override';
      caConflict: conflictStr := 'Conflict';
      caConflictCritical: conflictStr := 'Critical Conflict';
    else
      conflictStr := 'Unexpected';
    end;

    AddMessage(Format('%s conflict status: %s', [EditorID(e), conflictStr]));
  end;
end;

// Example 2: Find all conflicting records in plugin
var
  plugin: IwbFile;
  i, count, conflictCount: integer;
  rec: IwbMainRecord;
  conflictAll: integer;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    conflictCount := 0;

    AddMessage('Finding conflicting records...');

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        conflictAll := ConflictAllForMainRecord(rec);
        if (conflictAll = caConflict) or (conflictAll = caConflictCritical) then begin
          Inc(conflictCount);
          if conflictAll = caConflictCritical then
            AddMessage(Format('  CRITICAL: %s', [EditorID(rec)]))
          else
            AddMessage(Format('  Conflict: %s', [EditorID(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d conflicting record(s)', [conflictCount]));
  end;
end;

// Example 3: Categorize records by conflict type
var
  plugin: IwbFile;
  i, count: integer;
  rec: IwbMainRecord;
  conflictAll: integer;
  stats: array[0..6] of integer;
  ca: integer;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    for ca := caUnknown to caConflictCritical do
      stats[ca] := 0;

    count := RecordCount(plugin);
    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        conflictAll := ConflictAllForMainRecord(rec);
        Inc(stats[conflictAll]);
      end;
    end;

    AddMessage(Format('Conflict statistics for %s:', [GetFileName(plugin)]));
    AddMessage(Format('  Unknown: %d', [stats[caUnknown]]));
    AddMessage(Format('  Only One: %d', [stats[caOnlyOne]]));
    AddMessage(Format('  No Conflict: %d', [stats[caNoConflict]]));
    AddMessage(Format('  Benign Conflict: %d', [stats[caConflictBenign]]));
    AddMessage(Format('  Override: %d', [stats[caOverride]]));
    AddMessage(Format('  Conflict: %d', [stats[caConflict]]));
    AddMessage(Format('  Critical Conflict: %d', [stats[caConflictCritical]]));
  end;
end;

// Example 4: Check conflict status for override chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  conflictAll: integer;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    count := OverrideCount(masterRec);

    AddMessage(Format('Conflict analysis for %s:', [EditorID(masterRec)]));
    conflictAll := ConflictAllForMainRecord(masterRec);
    AddMessage(Format('  Master: %d', [conflictAll]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        conflictAll := ConflictAllForMainRecord(overrideRec);
        AddMessage(Format('  %s: %d',
          [GetFileName(GetFile(overrideRec)), conflictAll]));
      end;
    end;
  end;
end;
```

## See Also

- [ConflictThisForMainRecord](IwbMainRecord_ConflictThisForMainRecord.md)
- [ConflictAllForNode](IwbElement_ConflictAllForNode.md)
- [ConflictAllForElements](Global_ConflictAllForElements.md)

