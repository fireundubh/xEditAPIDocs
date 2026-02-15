# SetFormVCS2

## Syntax

```pascal
procedure SetFormVCS2(ARecord: IwbMainRecord; AValue: Cardinal);
```

## Description

Changes the native value of the `VCS2` property of `ARecord` to `AValue`

The `VCS2` property corresponds to the `Version Control Info 2` element in the Record Header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the version control info on |
| AValue | Cardinal | The new Version Control Info 2 value |

## Example

```pascal
// Example 1: Set VCS2 value on record
var
  newVCS2: Cardinal;
begin
  if Assigned(e) then begin
    newVCS2 := 99;
    SetFormVCS2(e, newVCS2);
    AddMessage(Format('%s: Set VCS2 to %d', [EditorID(e), newVCS2]));
  end;
end;

// Example 2: Copy both VCS values from source to target
var
  sourceRec: IwbMainRecord;
  sourceFile: IwbFile;
  fixedFormID: Cardinal;
  sourceVCS1, sourceVCS2: Cardinal;
begin
  if Assigned(e) then begin
    sourceFile := FileByIndex(0);
    if Assigned(sourceFile) then begin
      fixedFormID := FixedFormID(e);
      sourceRec := RecordByFormID(sourceFile, fixedFormID, false);

      if Assigned(sourceRec) then begin
        sourceVCS1 := GetFormVCS1(sourceRec);
        sourceVCS2 := GetFormVCS2(sourceRec);

        SetFormVCS1(e, sourceVCS1);
        SetFormVCS2(e, sourceVCS2);

        AddMessage(Format('Copied VCS stamps: VCS1=%d, VCS2=%d',
          [sourceVCS1, sourceVCS2]));
      end;
    end;
  end;
end;

// Example 3: Set timestamp-like VCS2 value
var
  timestamp: Cardinal;
begin
  if Assigned(e) then begin
    timestamp := DateTimeToUnix(Now);
    SetFormVCS2(e, timestamp);
    AddMessage(Format('%s: Set VCS2 timestamp to %d', [EditorID(e), timestamp]));
  end;
end;

// Example 4: Sync VCS2 across all overrides
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  masterVCS2: Cardinal;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    masterVCS2 := GetFormVCS2(masterRec);
    count := OverrideCount(masterRec);

    AddMessage(Format('Syncing VCS2=%d to %d override(s)...', [masterVCS2, count]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        SetFormVCS2(overrideRec, masterVCS2);
        AddMessage(Format('  Updated: %s', [GetFileName(GetFile(overrideRec))]));
      end;
    end;
  end;
end;
```

## See Also

- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md)
- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)


