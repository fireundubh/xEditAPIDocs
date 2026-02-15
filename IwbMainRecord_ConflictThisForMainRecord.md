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
// Example 1: Check specific record's conflict role
var
  conflictThis: TConflictThis;
  conflictStr: string;
begin
  if Assigned(e) then begin
    conflictThis := ConflictThisForMainRecord(e);

    case conflictThis of
      ctUnknown: conflictStr := 'Unknown';
      ctIgnored: conflictStr := 'Ignored';
      ctNotDefined: conflictStr := 'Not Defined';
      ctIdenticalToMaster: conflictStr := 'Identical to Master';
      ctOnlyOne: conflictStr := 'Only One';
      ctHiddenByModGroup: conflictStr := 'Hidden by Mod Group';
      ctMaster: conflictStr := 'Master';
      ctConflictBenign: conflictStr := 'Benign Conflict';
      ctOverride: conflictStr := 'Override';
      ctIdenticalToMasterWinsConflict: conflictStr := 'Identical to Master (Wins)';
      ctConflictWins: conflictStr := 'Conflict (Wins)';
      ctConflictLoses: conflictStr := 'Conflict (Loses)';
    else
      conflictStr := 'Unexpected';
    end;

    AddMessage(Format('%s in %s: %s',
      [EditorID(e), GetFileName(GetFile(e)), conflictStr]));
  end;
end;

// Example 2: Find winning and losing conflicts
var
  plugin: IwbFile;
  i, count, winsCount, losesCount: integer;
  rec: IwbMainRecord;
  conflictThis: TConflictThis;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    winsCount := 0;
    losesCount := 0;

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        conflictThis := ConflictThisForMainRecord(rec);
        if conflictThis = ctConflictWins then begin
          Inc(winsCount);
          AddMessage(Format('  Wins: %s', [EditorID(rec)]));
        end else if conflictThis = ctConflictLoses then begin
          Inc(losesCount);
          AddMessage(Format('  Loses: %s', [EditorID(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Wins: %d, Loses: %d', [winsCount, losesCount]));
  end;
end;

// Example 3: Check override chain conflict status
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  conflictThis: TConflictThis;
  statusStr: string;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    count := OverrideCount(masterRec);

    AddMessage(Format('Override chain conflict status for %s:', [EditorID(masterRec)]));

    conflictThis := ConflictThisForMainRecord(masterRec);
    AddMessage(Format('  Master in %s: %d',
      [GetFileName(GetFile(masterRec)), Ord(conflictThis)]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        conflictThis := ConflictThisForMainRecord(overrideRec);
        statusStr := '';
        if conflictThis = ctConflictWins then
          statusStr := ' (WINS)'
        else if conflictThis = ctConflictLoses then
          statusStr := ' (loses)';

        AddMessage(Format('  %s: %d%s',
          [GetFileName(GetFile(overrideRec)), Ord(conflictThis), statusStr]));
      end;
    end;
  end;
end;

// Example 4: Categorize all records by conflict status
var
  plugin: IwbFile;
  i, count: integer;
  rec: IwbMainRecord;
  conflictThis: TConflictThis;
  stats: array[TConflictThis] of integer;
  ct: TConflictThis;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    // Initialize counters
    for ct := Low(TConflictThis) to High(TConflictThis) do
      stats[ct] := 0;

    count := RecordCount(plugin);
    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        conflictThis := ConflictThisForMainRecord(rec);
        Inc(stats[conflictThis]);
      end;
    end;

    AddMessage(Format('Conflict breakdown for %s:', [GetFileName(plugin)]));
    AddMessage(Format('  Master: %d', [stats[ctMaster]]));
    AddMessage(Format('  Override: %d', [stats[ctOverride]]));
    AddMessage(Format('  Identical to Master: %d', [stats[ctIdenticalToMaster]]));
    AddMessage(Format('  Wins Conflict: %d', [stats[ctConflictWins]]));
    AddMessage(Format('  Loses Conflict: %d', [stats[ctConflictLoses]]));
    AddMessage(Format('  Benign Conflict: %d', [stats[ctConflictBenign]]));
    AddMessage(Format('  Only One: %d', [stats[ctOnlyOne]]));
  end;
end;
```

