# WinningOverride

## Syntax

```pascal
function WinningOverride(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the final overriding record in the current load order.

This function retrieves the WinningOverride property, which returns the last record in the override chain (the one with the highest load order that modifies this FormID). If the record has no overrides, returns the record itself. This is the "active" version of the record that the game will use. Unlike HighestOverrideOrSelf, this always returns the absolute last override regardless of load order position.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the winning override from |

## Returns

Returns the last loaded overriding IwbMainRecord, or the record itself if no overrides exist.

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
      masterValue := GetElementEditValue(e, 'DATA\Value');
      winningValue := GetElementEditValue(winningRec, 'DATA\Value');

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
      SetElementEditValue(winningRec, 'FULL', 'Modified Display Name');
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


