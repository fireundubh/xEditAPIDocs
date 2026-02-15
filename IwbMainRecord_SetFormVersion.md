# SetFormVersion

## Syntax

```pascal
procedure SetFormVersion(ARecord: IwbMainRecord; AVersion: Cardinal);
```

## Description

Changes the native value of the `Version` property of `ARecord` to `AVersion`

The `Version` property corresponds to the `Form Version` element in the Record Header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the form version on |
| AVersion | Cardinal | The new form version value |

## Example

```pascal
// Example 1: Update form version to specific value
var
  currentVersion, newVersion: Cardinal;
begin
  if Assigned(e) then begin
    currentVersion := GetFormVersion(e);
    newVersion := 44;

    if currentVersion <> newVersion then begin
      SetFormVersion(e, newVersion);
      AddMessage(Format('%s: Updated form version from %d to %d',
        [EditorID(e), currentVersion, newVersion]));
    end else begin
      AddMessage(Format('%s: Already at version %d', [EditorID(e), newVersion]));
    end;
  end;
end;

// Example 2: Batch update all records to target version
var
  plugin: IwbFile;
  i, count, updatedCount: integer;
  rec: IwbMainRecord;
  currentVersion, targetVersion: Cardinal;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    targetVersion := 44;
    count := RecordCount(plugin);
    updatedCount := 0;

    AddMessage(Format('Updating form versions to %d...', [targetVersion]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        currentVersion := GetFormVersion(rec);
        if currentVersion < targetVersion then begin
          SetFormVersion(rec, targetVersion);
          Inc(updatedCount);
          AddMessage(Format('  Updated: %s (was %d)', [EditorID(rec), currentVersion]));
        end;
      end;
    end;

    AddMessage(Format('Updated %d record(s)', [updatedCount]));
  end;
end;

// Example 3: Increment form version
var
  currentVersion, newVersion: Cardinal;
begin
  if Assigned(e) then begin
    currentVersion := GetFormVersion(e);
    newVersion := currentVersion + 1;

    SetFormVersion(e, newVersion);
    AddMessage(Format('%s: Incremented version from %d to %d',
      [EditorID(e), currentVersion, newVersion]));
  end;
end;

// Example 4: Sync form version across override chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  masterVersion: Cardinal;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    masterVersion := GetFormVersion(masterRec);
    count := OverrideCount(masterRec);

    AddMessage(Format('Syncing form versions to master version %d...', [masterVersion]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        if GetFormVersion(overrideRec) <> masterVersion then begin
          SetFormVersion(overrideRec, masterVersion);
          AddMessage(Format('  Updated: %s', [GetFileName(GetFile(overrideRec))]));
        end;
      end;
    end;
  end;
end;
```

## See Also

- [GetFormVersion](IwbMainRecord_GetFormVersion.md)


