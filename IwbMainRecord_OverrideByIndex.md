# OverrideByIndex

## Syntax

```pascal
function OverrideByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the override at `AIndex` in the override list of `ARecord`.

The list is stored on the master. An override has an empty list, so pass the master or [MasterOrSelf](IwbMainRecord_MasterOrSelf.md). Entries are ordered by load order, lowest first. Index 0 is the first override, not the master. The master itself is not in the list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The master record that owns the override list. An override returns nil |
| AIndex | integer | The zero-based index of the override, lowest load order first |

## Returns

Returns the override at `AIndex`, or nil when the index is out of range, `ARecord` is not the master, or `ARecord` is not a main record.

## Example

```pascal
// Example 1: List all plugins that override a record
var
  overrideRec: IwbMainRecord;
  i, count: integer;
  overrideFile: IwbFile;
begin
  if Assigned(e) then begin
    count := OverrideCount(MasterOrSelf(e));
    AddMessage(Format('%s is overridden by %d file(s):', [EditorID(e), count]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(MasterOrSelf(e), i);
      if Assigned(overrideRec) then begin
        overrideFile := GetFile(overrideRec);
        AddMessage(Format('  [%d] %s', [i, GetFileName(overrideFile)]));
      end;
    end;
  end;
end;

// Example 2: Find first override that changes specific field
var
  overrideRec: IwbMainRecord;
  i, count: integer;
  masterValue, overrideValue: string;
begin
  if Assigned(e) then begin
    masterValue := GetElementEditValues(MasterOrSelf(e), 'DATA\Value');
    count := OverrideCount(MasterOrSelf(e));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(MasterOrSelf(e), i);
      if Assigned(overrideRec) then begin
        overrideValue := GetElementEditValues(overrideRec, 'DATA\Value');
        if overrideValue <> masterValue then begin
          AddMessage(Format('First value change in: %s',
            [GetFileName(GetFile(overrideRec))]));
          AddMessage(Format('  Changed from %s to %s', [masterValue, overrideValue]));
          Break;
        end;
      end;
    end;
  end;
end;

// Example 3: Apply changes to all overrides in chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  newKeyword: string;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    newKeyword := '0010A8A6'; // ArmorLight keyword
    count := OverrideCount(masterRec);

    AddMessage(Format('Adding keyword to master and %d override(s)...', [count]));

    // Process master
    SetElementEditValues(masterRec, 'KWDA\[0]', newKeyword);

    // Process all overrides
    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        SetElementEditValues(overrideRec, 'KWDA\[0]', newKeyword);
        AddMessage(Format('  Updated: %s', [GetFileName(GetFile(overrideRec))]));
      end;
    end;
  end;
end;

// Example 4: Build override history showing all changes
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  history: TStringList;
  currentValue, prevValue: string;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    history := TStringList.Create;
    try
      prevValue := GetElementEditValues(masterRec, 'FULL');
      history.Add(Format('[Master] %s: "%s"',
        [GetFileName(GetFile(masterRec)), prevValue]));

      count := OverrideCount(masterRec);
      for i := 0 to count - 1 do begin
        overrideRec := OverrideByIndex(masterRec, i);
        if Assigned(overrideRec) then begin
          currentValue := GetElementEditValues(overrideRec, 'FULL');
          if currentValue <> prevValue then begin
            history.Add(Format('[%d] %s: "%s" (changed)',
              [i, GetFileName(GetFile(overrideRec)), currentValue]));
            prevValue := currentValue;
          end else begin
            history.Add(Format('[%d] %s: "%s"',
              [i, GetFileName(GetFile(overrideRec)), currentValue]));
          end;
        end;
      end;

      AddMessage('Override history for ' + EditorID(masterRec) + ':');
      for i := 0 to history.Count - 1 do
        AddMessage(history[i]);
    finally
      history.Free;
    end;
  end;
end;
```

## See Also

- [OverrideCount](IwbMainRecord_OverrideCount.md)
- [Master](IwbMainRecord_Master.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


