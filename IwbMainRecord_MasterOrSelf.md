# MasterOrSelf

## Syntax

```pascal
function MasterOrSelf(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record overridden by `ARecord`, or the overriding record itself

**Note:** Unlike [Master](IwbMainRecord_Master.md), the return value from this function will always be assigned.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get the master or itself from |

## Returns

Returns the master IwbMainRecord if the record is an override, or the record itself if it is the master.

## Example

```pascal
// Example 1: Get master record for processing (guaranteed non-nil)
var
  masterRec: IwbMainRecord;
  masterFile: IwbFile;
begin
  if Assigned(e) then begin
    masterRec := MasterOrSelf(e);
    // masterRec is always assigned, safe to use
    masterFile := GetFile(masterRec);

    if Equals(e, masterRec) then
      AddMessage(Format('%s is the master record', [EditorID(e)]))
    else
      AddMessage(Format('%s overrides master from %s',
        [EditorID(e), GetFileName(masterFile)]));
  end;
end;

// Example 2: Process all overrides starting from any record in chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    // Get the master regardless of where we start
    masterRec := MasterOrSelf(e);

    AddMessage(Format('Processing override chain for %s', [EditorID(masterRec)]));
    count := OverrideCount(masterRec);

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then
        AddMessage(Format('  Override %d: %s', [i, GetFileName(GetFile(overrideRec))]));
    end;
  end;
end;

// Example 3: Get original FormID from any record in override chain
var
  masterRec: IwbMainRecord;
  originalFormID: Cardinal;
begin
  if Assigned(e) then begin
    masterRec := MasterOrSelf(e);
    originalFormID := FormID(masterRec);

    AddMessage(Format('Original FormID: %s (from %s)',
      [IntToHex(originalFormID, 8), GetFileName(GetFile(masterRec))]));
  end;
end;

// Example 4: Copy data from master without checking if override exists
var
  masterRec: IwbMainRecord;
  masterValue: string;
begin
  if Assigned(e) then begin
    masterRec := MasterOrSelf(e);
    // No need to check if nil - always assigned

    masterValue := GetElementEditValue(masterRec, 'FULL - Name');
    if masterValue <> '' then
      AddMessage(Format('Master name: %s', [masterValue]));
  end;
end;
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


