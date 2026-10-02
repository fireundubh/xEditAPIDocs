# Master

## Syntax

```pascal
function Master(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record that `ARecord` overrides.

Every override in the chain points at that same master: the record that owns the override list, not the previous override. Calling `Master` on the result returns nil. Returns nil when `ARecord` is itself the master, or when `ARecord` is not a main record. Use [MasterOrSelf](IwbMainRecord_MasterOrSelf.md) when the caller may already be holding the master.

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
      masterValue := GetElementEditValues(masterRec, 'DATA\Value');
      overrideValue := GetElementEditValues(e, 'DATA\Value');

      AddMessage(Format('Master value: %s', [masterValue]));
      AddMessage(Format('Override value: %s', [overrideValue]));

      if masterValue <> overrideValue then
        AddMessage('Override changes value')
      else
        AddMessage('Override keeps same value');
    end;
  end;
end;

// Example 3: The master is the base record, not the previous override
var
  masterRec: IwbMainRecord;
begin
  if Assigned(e) then begin
    masterRec := Master(e);
    if Assigned(masterRec) then begin
      AddMessage(Format('Base master in %s', [GetFileName(GetFile(masterRec))]));
      AddMessage(Format('Override count on that master: %d', [OverrideCount(masterRec)]));
    end else
      AddMessage(EditorID(e) + ' is the master');
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
      masterScript := GetElementEditValues(masterRec, 'VMAD - Virtual Machine Adapter');
      if masterScript <> '' then begin
        SetElementEditValues(e, 'VMAD - Virtual Machine Adapter', masterScript);
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


