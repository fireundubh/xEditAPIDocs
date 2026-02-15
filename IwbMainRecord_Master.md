# Master

## Syntax

```pascal
function Master(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record that this record directly overrides.

This function retrieves the Master property, which returns the immediate parent record in the override chain (the record from a higher-priority file that this record modifies). Returns nil if this record is itself a master (not an override of anything). For records with multiple levels of overrides, this returns only the direct parent, not the original master.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The overriding record to get the master from |

## Returns

Returns the master IwbMainRecord that is overridden, or Nil if the record is not an override.

## Example

```pascal
// Example 1: Check if record is an override and get its master
var
  masterRec: IwbMainRecord;
  masterFile: IwbFile;
begin
  if Assigned(e) then begin
    masterRec := Master(e);
    if Assigned(masterRec) then begin
      masterFile := GetFile(masterRec);
      AddMessage(Format('%s overrides record from %s',
        [EditorID(e), GetFileName(masterFile)]));
    end else begin
      AddMessage(EditorID(e) + ' is a master record (not an override)');
    end;
  end;
end;

// Example 2: Compare override with its master
var
  masterRec: IwbMainRecord;
  overrideValue, masterValue: string;
begin
  if Assigned(e) then begin
    masterRec := Master(e);
    if Assigned(masterRec) then begin
      masterValue := GetElementEditValue(masterRec, 'DATA\Value');
      overrideValue := GetElementEditValue(e, 'DATA\Value');

      AddMessage(Format('Master value: %s', [masterValue]));
      AddMessage(Format('Override value: %s', [overrideValue]));

      if masterValue <> overrideValue then
        AddMessage('Override changes value')
      else
        AddMessage('Override keeps same value');
    end;
  end;
end;

// Example 3: Walk the override chain to find original master
var
  currentRec, masterRec: IwbMainRecord;
  chain: string;
begin
  if Assigned(e) then begin
    currentRec := e;
    chain := GetFileName(GetFile(currentRec));

    // Walk backwards through override chain
    while Assigned(currentRec) do begin
      masterRec := Master(currentRec);
      if Assigned(masterRec) then begin
        chain := GetFileName(GetFile(masterRec)) + ' -> ' + chain;
        currentRec := masterRec;
      end else begin
        AddMessage('Override chain: ' + chain);
        AddMessage(Format('Original master in: %s', [GetFileName(GetFile(currentRec))]));
        Break;
      end;
    end;
  end;
end;

// Example 4: Copy field from master to override
var
  masterRec: IwbMainRecord;
  masterScript: string;
begin
  if Assigned(e) then begin
    masterRec := Master(e);
    if Assigned(masterRec) then begin
      masterScript := GetElementEditValue(masterRec, 'VMAD - Virtual Machine Adapter');
      if masterScript <> '' then begin
        SetElementEditValue(e, 'VMAD - Virtual Machine Adapter', masterScript);
        AddMessage('Copied script data from master');
      end;
    end;
  end;
end;
```

## See Also

- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [OverrideCount](IwbMainRecord_OverrideCount.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)


