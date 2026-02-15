# OverrideByIndex

## Syntax

```pascal
function OverrideByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the override record at the specified index in the override list.

This function accesses the Overrides property by index, providing array-style access to all records overriding this record. Overrides are ordered by load order (lowest to highest). Index 0 is the first override, not the master. Use OverrideCount to get the valid index range. Returns nil for invalid indices. Useful for iterating through the entire override chain.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The master record to get the override from |
| AIndex | integer | The zero-based index of the override in the override list |

## Returns

Returns the IwbMainRecord override at the specified index.

## Example

```pascal
// Example 1: List all plugins that override a record
var
  overrideRec: IwbMainRecord;
  i, count: integer;
  overrideFile: IwbFile;
begin
  if Assigned(e) then begin
    count := OverrideCount(e);
    AddMessage(Format('%s is overridden by %d file(s):', [EditorID(e), count]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(e, i);
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
    masterValue := GetElementEditValue(e, 'DATA\Value');
    count := OverrideCount(e);

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(e, i);
      if Assigned(overrideRec) then begin
        overrideValue := GetElementEditValue(overrideRec, 'DATA\Value');
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
    SetElementEditValue(masterRec, 'KWDA\[0]', newKeyword);

    // Process all overrides
    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        SetElementEditValue(overrideRec, 'KWDA\[0]', newKeyword);
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
      prevValue := GetElementEditValue(masterRec, 'FULL');
      history.Add(Format('[Master] %s: "%s"',
        [GetFileName(GetFile(masterRec)), prevValue]));

      count := OverrideCount(masterRec);
      for i := 0 to count - 1 do begin
        overrideRec := OverrideByIndex(masterRec, i);
        if Assigned(overrideRec) then begin
          currentValue := GetElementEditValue(overrideRec, 'FULL');
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


