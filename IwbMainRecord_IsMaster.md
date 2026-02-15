# IsMaster

## Syntax

```pascal
function IsMaster(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record is a master (original) record rather than an override.

This function retrieves the IsMaster property, which returns true if the record is the original definition (not overriding another record from a master file). Master records are the first in their override chain. Returns false for override records or invalid inputs. Note: This refers to the record's position in the override chain, not whether it's in a master file (.esm).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check if it is a master record |

## Returns

Returns `True` if the record is a master record, `False` otherwise.

## Example

```pascal
// Example 1: Identify master vs override records
var
  recFile: IwbFile;
begin
  if Assigned(e) then begin
    recFile := GetFile(e);
    if IsMaster(e) then
      AddMessage(Format('%s is a master record in %s',
        [EditorID(e), GetFileName(recFile)]))
    else
      AddMessage(Format('%s is an override in %s',
        [EditorID(e), GetFileName(recFile)]));
  end;
end;

// Example 2: Process only master records in a file
var
  plugin: IwbFile;
  i, count, masterCount: integer;
  rec: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    masterCount := 0;

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and IsMaster(rec) then begin
        Inc(masterCount);
        AddMessage(Format('Master: %s', [EditorID(rec)]));
      end;
    end;

    AddMessage(Format('Found %d master records', [masterCount]));
  end;
end;

// Example 3: Skip override processing if record is master
var
  masterRec: IwbMainRecord;
begin
  if Assigned(e) then begin
    if IsMaster(e) then begin
      AddMessage('Record is a master - processing original definition');
      // Process master record...
    end else begin
      masterRec := Master(e);
      if Assigned(masterRec) then
        AddMessage(Format('Override of master in %s',
          [GetFileName(GetFile(masterRec))]));
    end;
  end;
end;

// Example 4: Count masters vs overrides in plugin
var
  plugin: IwbFile;
  i, count, masters, overrides: integer;
  rec: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    masters := 0;
    overrides := 0;

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        if IsMaster(rec) then
          Inc(masters)
        else
          Inc(overrides);
      end;
    end;

    AddMessage(Format('%s: %d masters, %d overrides',
      [GetFileName(plugin), masters, overrides]));
  end;
end;
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)


