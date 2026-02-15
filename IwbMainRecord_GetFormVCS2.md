# GetFormVCS2

## Syntax

```pascal
function GetFormVCS2(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the native value of the `Version Control Info 2` element

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the version control info from |

## Returns

Returns the Version Control Info 2 value as a Cardinal.

## Example

```pascal
// Example 1: Retrieve and display VCS2 value
var
  vcs2: Cardinal;
begin
  if Assigned(e) then begin
    vcs2 := GetFormVCS2(e);
    AddMessage(Format('%s Version Control Info 2: %d', [EditorID(e), vcs2]));
  end;
end;

// Example 2: Copy both VCS values from source record
var
  sourceRec: IwbMainRecord;
  sourceFile: IwbFile;
  fixedFormID: Cardinal;
  vcs1, vcs2: Cardinal;
begin
  if Assigned(e) then begin
    sourceFile := FileByIndex(0);
    if Assigned(sourceFile) then begin
      fixedFormID := FixedFormID(e);
      sourceRec := RecordByFormID(sourceFile, fixedFormID, false);

      if Assigned(sourceRec) then begin
        vcs1 := GetFormVCS1(sourceRec);
        vcs2 := GetFormVCS2(sourceRec);

        SetFormVCS1(e, vcs1);
        SetFormVCS2(e, vcs2);

        AddMessage(Format('Copied VCS stamps to %s: VCS1=%d, VCS2=%d',
          [EditorID(e), vcs1, vcs2]));
      end;
    end;
  end;
end;

// Example 3: Find records with specific VCS2 value
var
  plugin: IwbFile;
  i, count, matchCount: integer;
  rec: IwbMainRecord;
  vcs2, targetVCS2: Cardinal;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    targetVCS2 := 12345; // Example value
    count := RecordCount(plugin);
    matchCount := 0;

    AddMessage(Format('Finding records with VCS2 = %d...', [targetVCS2]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        vcs2 := GetFormVCS2(rec);
        if vcs2 = targetVCS2 then begin
          Inc(matchCount);
          AddMessage(Format('  %s (%s)', [EditorID(rec), Signature(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d matching record(s)', [matchCount]));
  end;
end;
```

## See Also

- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)
- [SetFormVCS2](IwbMainRecord_SetFormVCS2.md)


