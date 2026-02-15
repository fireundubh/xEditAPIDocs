# SetFormVCS1

## Syntax

```pascal
procedure SetFormVCS1(ARecord: IwbMainRecord; AValue: Cardinal);
```

## Description

Changes the native value of the `VCS1` property of `ARecord` to `AValue`

The `VCS1` property corresponds to the `Version Control Info 1` element in the Record Header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the version control info on |
| AValue | Cardinal | The new Version Control Info 1 value |

## Example

```pascal
// Example 1: Set VCS1 value on record
var
  newVCS1: Cardinal;
begin
  if Assigned(e) then begin
    newVCS1 := 42;
    SetFormVCS1(e, newVCS1);
    AddMessage(Format('%s: Set VCS1 to %d', [EditorID(e), newVCS1]));
  end;
end;

// Example 2: Copy VCS1 from master to override
var
  masterRec: IwbMainRecord;
  masterFile: IwbFile;
  fixedFormID: Cardinal;
  masterVCS1: Cardinal;
begin
  if Assigned(e) then begin
    masterFile := FileByIndex(0);
    if Assigned(masterFile) then begin
      fixedFormID := FixedFormID(e);
      masterRec := RecordByFormID(masterFile, fixedFormID, false);

      if Assigned(masterRec) then begin
        masterVCS1 := GetFormVCS1(masterRec);
        SetFormVCS1(e, masterVCS1);
        AddMessage(Format('Synchronized VCS1: %d', [masterVCS1]));
      end;
    end;
  end;
end;

// Example 3: Increment VCS1 value
var
  currentVCS1, newVCS1: Cardinal;
begin
  if Assigned(e) then begin
    currentVCS1 := GetFormVCS1(e);
    newVCS1 := currentVCS1 + 1;

    SetFormVCS1(e, newVCS1);
    AddMessage(Format('%s: Incremented VCS1 from %d to %d',
      [EditorID(e), currentVCS1, newVCS1]));
  end;
end;

// Example 4: Batch update VCS1 for all records in plugin
var
  plugin: IwbFile;
  i, count, updatedCount: integer;
  rec: IwbMainRecord;
  standardVCS1: Cardinal;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    standardVCS1 := 100;
    count := RecordCount(plugin);
    updatedCount := 0;

    AddMessage(Format('Setting VCS1 to %d for all records...', [standardVCS1]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        SetFormVCS1(rec, standardVCS1);
        Inc(updatedCount);
      end;
    end;

    AddMessage(Format('Updated %d record(s)', [updatedCount]));
  end;
end;
```

## See Also

- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md)
- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS2](IwbMainRecord_SetFormVCS2.md)


