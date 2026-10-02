# WinningOverride

## Syntax

```pascal
function WinningOverride(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the winning override of `ARecord`.

The winning override is the last non-partial record in load order. If every override is partial, or there are no overrides, the master itself is returned. Calling this on any record in the chain returns that same record. Returns nil when `ARecord` is not a main record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the winning override from |

## Returns

Returns the winning non-partial record, or the master when no such override exists. Returns nil when `ARecord` is not a main record.

## Example

```pascal
// Example 1: Get the active version of a record
var
  winningRec: IwbMainRecord;
  winningPlugin: string;
begin
  if Assigned(e) then begin
    winningRec := WinningOverride(e);
    if Assigned(winningRec) then begin
      winningPlugin := GetFileName(GetFile(winningRec));
      AddMessage(Format('Winning override in: %s', [winningPlugin]));
    end;
  end;
end;

// Example 2: Compare master vs winning override values
var
  winningRec: IwbMainRecord;
  masterValue, winningValue: string;
begin
  if Assigned(e) then begin
    winningRec := WinningOverride(e);
    if Assigned(winningRec) then begin
      masterValue := GetElementEditValues(e, 'DATA\Value');
      winningValue := GetElementEditValues(winningRec, 'DATA\Value');

      if masterValue <> winningValue then
        AddMessage(Format('%s: Value changed from %s to %s',
          [EditorID(e), masterValue, winningValue]));
    end;
  end;
end;

// Example 3: Edit winning override instead of master
var
  winningRec: IwbMainRecord;
begin
  if Assigned(e) then begin
    winningRec := WinningOverride(e);
    if Assigned(winningRec) then begin
      // Always modify the winning override, not the master
      SetElementEditValues(winningRec, 'FULL', 'Modified Display Name');
      AddMessage(Format('Modified winning override in %s',
        [GetFileName(GetFile(winningRec))]));
    end;
  end;
end;

// Example 4: Check if record is being overridden
var
  winningRec: IwbMainRecord;
  recFile, winningFile: IwbFile;
begin
  if Assigned(e) then begin
    winningRec := WinningOverride(e);
    if Assigned(winningRec) then begin
      recFile := GetFile(e);
      winningFile := GetFile(winningRec);

      if recFile <> winningFile then
        AddMessage(Format('%s is overridden by %s',
          [GetFileName(recFile), GetFileName(winningFile)]))
      else
        AddMessage('Record is not overridden');
    end;
  end;
end;
```

## See Also

- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)
- [Master](IwbMainRecord_Master.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)


