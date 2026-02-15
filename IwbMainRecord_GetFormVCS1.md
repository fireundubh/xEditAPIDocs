# GetFormVCS1

## Syntax

```pascal
function GetFormVCS1(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the native value of the `Version Control Info 1` element

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the version control info from |

## Returns

Returns the Version Control Info 1 value as a Cardinal.

## Example

```pascal
// Example 1: Copy version control stamps from master to override
var
  masterRec: IwbMainRecord;
  masterFile: IwbFile;
  fixedFormID: Cardinal;
  vcs1: Cardinal;
begin
  if Assigned(e) then begin
    masterFile := FileByIndex(0);
    if Assigned(masterFile) then begin
      fixedFormID := FixedFormID(e);
      masterRec := RecordByFormID(masterFile, fixedFormID, false);

      if Assigned(masterRec) then begin
        vcs1 := GetFormVCS1(masterRec);
        SetFormVCS1(e, vcs1);
        AddMessage(Format('Copied VCS1 stamp: %d', [vcs1]));
      end;
    end;
  end;
end;

// Example 2: Display version control information
var
  vcs1, vcs2: Cardinal;
begin
  if Assigned(e) then begin
    vcs1 := GetFormVCS1(e);
    vcs2 := GetFormVCS2(e);

    AddMessage(Format('%s version control info:', [EditorID(e)]));
    AddMessage(Format('  VCS1: %d', [vcs1]));
    AddMessage(Format('  VCS2: %d', [vcs2]));
  end;
end;

// Example 3: Sync VCS stamps across override chain
var
  masterRec, overrideRec: IwbMainRecord;
  i, count: integer;
  masterVCS1, masterVCS2: Cardinal;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    masterVCS1 := GetFormVCS1(masterRec);
    masterVCS2 := GetFormVCS2(masterRec);
    count := OverrideCount(masterRec);

    AddMessage(Format('Syncing VCS stamps from master (VCS1=%d, VCS2=%d)...',
      [masterVCS1, masterVCS2]));

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        SetFormVCS1(overrideRec, masterVCS1);
        SetFormVCS2(overrideRec, masterVCS2);
        AddMessage(Format('  Updated: %s', [GetFileName(GetFile(overrideRec))]));
      end;
    end;
  end;
end;
```

## See Also

- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)
- [SetFormVCS2](IwbMainRecord_SetFormVCS2.md)


