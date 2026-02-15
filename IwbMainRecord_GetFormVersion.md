# GetFormVersion

## Syntax

```pascal
function GetFormVersion(ARecord: IwbMainRecord): Cardinal;
```

## Description

Return the native value of the Form Version element from the Record Header of `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the form version from |

## Returns

Returns the form version as a Cardinal value.

## Example

```pascal
// Example 1: Check record form version
var
  formVersion: Cardinal;
begin
  if Assigned(e) then begin
    formVersion := GetFormVersion(e);
    AddMessage(Format('%s has form version: %d', [EditorID(e), formVersion]));

    if formVersion >= 44 then
      AddMessage('  Uses Fallout 4 1.10+ format')
    else if formVersion >= 40 then
      AddMessage('  Uses Fallout 4 base format')
    else
      AddMessage('  Uses older format');
  end;
end;

// Example 2: Find records with specific form version
var
  plugin: IwbFile;
  i, count, matchCount: integer;
  rec: IwbMainRecord;
  formVersion, targetVersion: Cardinal;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    targetVersion := 44;
    count := RecordCount(plugin);
    matchCount := 0;

    AddMessage(Format('Finding records with form version %d...', [targetVersion]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        formVersion := GetFormVersion(rec);
        if formVersion = targetVersion then begin
          Inc(matchCount);
          AddMessage(Format('  %s (%s)', [EditorID(rec), Signature(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d record(s) with version %d', [matchCount, targetVersion]));
  end;
end;

// Example 3: Compare form versions across override chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  masterVersion, overrideVersion: Cardinal;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    masterVersion := GetFormVersion(masterRec);
    count := OverrideCount(masterRec);

    AddMessage(Format('%s form version history:', [EditorID(masterRec)]));
    AddMessage(Format('  Master version: %d', [masterVersion]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        overrideVersion := GetFormVersion(overrideRec);
        if overrideVersion <> masterVersion then
          AddMessage(Format('  %s: version %d (changed)',
            [GetFileName(GetFile(overrideRec)), overrideVersion]))
        else
          AddMessage(Format('  %s: version %d',
            [GetFileName(GetFile(overrideRec)), overrideVersion]));
      end;
    end;
  end;
end;

// Example 4: Statistics on form versions in plugin
var
  plugin: IwbFile;
  i, count: integer;
  rec: IwbMainRecord;
  formVersion: Cardinal;
  versionCounts: TStringList;
  idx: integer;
  versionStr: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    versionCounts := TStringList.Create;
    try
      count := RecordCount(plugin);

      for i := 0 to count - 1 do begin
        rec := RecordByIndex(plugin, i);
        if Assigned(rec) then begin
          formVersion := GetFormVersion(rec);
          versionStr := IntToStr(formVersion);
          idx := versionCounts.IndexOf(versionStr);
          if idx >= 0 then
            versionCounts.Objects[idx] := TObject(Integer(versionCounts.Objects[idx]) + 1)
          else
            versionCounts.AddObject(versionStr, TObject(1));
        end;
      end;

      AddMessage(Format('Form version distribution in %s:', [GetFileName(plugin)]));
      for i := 0 to versionCounts.Count - 1 do
        AddMessage(Format('  Version %s: %d record(s)',
          [versionCounts[i], Integer(versionCounts.Objects[i])]));
    finally
      versionCounts.Free;
    end;
  end;
end;
```

## See Also

- [SetFormVersion](IwbMainRecord_SetFormVersion.md)


