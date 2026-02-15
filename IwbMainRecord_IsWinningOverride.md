# IsWinningOverride

## Syntax

```pascal
function IsWinningOverride(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` loads last in the current load order

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check if it is the winning override |

## Returns

Returns `True` if the record loads last in the current load order, `False` otherwise.

## Example

```pascal
// Example 1: Check if record is the active version
var
  recFile: IwbFile;
begin
  if Assigned(e) then begin
    recFile := GetFile(e);
    if IsWinningOverride(e) then
      AddMessage(Format('%s in %s is the winning override (game uses this version)',
        [EditorID(e), GetFileName(recFile)]))
    else
      AddMessage(Format('%s in %s is not winning (game uses different version)',
        [EditorID(e), GetFileName(recFile)]));
  end;
end;

// Example 2: Only process records that will affect the game
var
  plugin: IwbFile;
  i, count, winningCount: integer;
  rec: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    winningCount := 0;

    AddMessage(Format('Finding winning overrides in %s...', [GetFileName(plugin)]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and IsWinningOverride(rec) then begin
        Inc(winningCount);
        AddMessage(Format('  %s (active in game)', [EditorID(rec)]));
      end;
    end;

    AddMessage(Format('Total winning overrides: %d', [winningCount]));
  end;
end;

// Example 3: Warn when editing non-winning override
var
  winningRec: IwbMainRecord;
  recFile, winningFile: IwbFile;
begin
  if Assigned(e) then begin
    if not IsWinningOverride(e) then begin
      winningRec := WinningOverride(e);
      if Assigned(winningRec) then begin
        recFile := GetFile(e);
        winningFile := GetFile(winningRec);
        AddMessage(Format('WARNING: Editing %s in %s',
          [EditorID(e), GetFileName(recFile)]));
        AddMessage(Format('But winning override is in %s',
          [GetFileName(winningFile)]));
        AddMessage('Your changes will NOT affect the game!');
      end;
    end else begin
      AddMessage('Record is winning - changes will affect game');
    end;
  end;
end;

// Example 4: Find which plugin wins for a FormID
var
  overrideRec: IwbMainRecord;
  i, count: integer;
  winningFile: string;
begin
  if Assigned(e) then begin
    count := OverrideCount(e);
    AddMessage(Format('Checking %d overrides for %s...', [count, EditorID(e)]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(e, i);
      if Assigned(overrideRec) then begin
        if IsWinningOverride(overrideRec) then begin
          winningFile := GetFileName(GetFile(overrideRec));
          AddMessage(Format('Winner: %s', [winningFile]));
          Break;
        end;
      end;
    end;
  end;
end;
```

## See Also

- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


