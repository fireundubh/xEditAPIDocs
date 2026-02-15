# FixedFormID

## Syntax

```pascal
function FixedFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the File Form IDof `ARecord`, clamping the Mod ID to the number of master files for the containing file

Local records will not have a load order prefix (e.g., `0x00FFFFFF`) and overrides will have a prefix relative to the record's file's masters.

This function can be used in the resolution of HITME issues.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the fixed Form ID from |

## Returns

Returns the File Form ID with the Mod ID clamped to the master file count.

## Example

```pascal
// Example 1: Copy version control stamps between override and master
var
  masterRec: IwbMainRecord;
  masterFile: IwbFile;
  fixedFormID: Cardinal;
begin
  if Assigned(e) then begin
    masterFile := FileByIndex(0);
    if Assigned(masterFile) then begin
      fixedFormID := FixedFormID(e);
      masterRec := RecordByFormID(masterFile, fixedFormID, false);

      if Assigned(masterRec) then begin
        SetFormVCS1(e, GetFormVCS1(masterRec));
        SetFormVCS2(e, GetFormVCS2(masterRec));
        AddMessage('Copied version control stamps from master');
      end;
    end;
  end;
end;

// Example 2: Compare FixedFormID vs LoadOrderFormID
var
  fixedFormID, loadOrderFormID: Cardinal;
  fixedIndex, loadOrderIndex: byte;
begin
  if Assigned(e) then begin
    fixedFormID := FixedFormID(e);
    loadOrderFormID := GetLoadOrderFormID(e);

    fixedIndex := fixedFormID shr 24;
    loadOrderIndex := loadOrderFormID shr 24;

    AddMessage(Format('Fixed FormID:      %s (master index: %d)', [IntToHex(fixedFormID, 8), fixedIndex]));
    AddMessage(Format('Load Order FormID: %s (LO index: %d)', [IntToHex(loadOrderFormID, 8), loadOrderIndex]));
  end;
end;

// Example 3: Resolve record in original master file
var
  originalRec: IwbMainRecord;
  masterFile: IwbFile;
  fixedFormID: Cardinal;
begin
  if Assigned(e) then begin
    // Get the first master (original source)
    masterFile := MasterByIndex(GetFile(e), 0);
    if Assigned(masterFile) then begin
      fixedFormID := FixedFormID(e);
      originalRec := RecordByFormID(masterFile, fixedFormID, false);

      if Assigned(originalRec) then
        AddMessage(Format('Original record: %s in %s',
          [EditorID(originalRec), GetFileName(masterFile)]))
      else
        AddMessage('Record not found in master file');
    end;
  end;
end;

// Example 4: Check if record is local to its file
var
  fixedFormID: Cardinal;
  fileIndex: byte;
begin
  if Assigned(e) then begin
    fixedFormID := FixedFormID(e);
    fileIndex := fixedFormID shr 24;

    if fileIndex = 0 then
      AddMessage(Format('%s is a local record (FormID: %s)',
        [EditorID(e), IntToHex(fixedFormID, 8)]))
    else
      AddMessage(Format('%s references master %d (FormID: %s)',
        [EditorID(e), fileIndex, IntToHex(fixedFormID, 8)]));
  end;
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)


