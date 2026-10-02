# FixedFormID

## Syntax

```pascal
function FixedFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the file FormID of `ARecord`. If the stored slot is past the count of masters of the same module type, it is clamped to the file's own module index. Overrides keep a prefix that selects one of that file's masters. For a full plugin, a local record uses the file's own index, which is the number of full masters, not `00` (`00` is the first master, and only a file with no masters stores its own records as `00`). The value does not follow the current load order. This function can be used in the resolution of HITME issues. Returns 0 when `ARecord` is not a main record.

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

// Example 4: Check if a full-plugin record is local to its file
var
  fixedFormID: Cardinal;
  fileIndex: byte;
  recFile: IwbFile;
begin
  if Assigned(e) then begin
    recFile := GetFile(e);
    fixedFormID := FixedFormID(e);

    if Assigned(recFile) and not GetIsLight(recFile) and not GetIsMedium(recFile) then begin
      fileIndex := fixedFormID shr 24;

      if fileIndex = MasterCount(recFile) then
        AddMessage(Format('%s is a local record (FormID: %s)',
          [EditorID(e), IntToHex(fixedFormID, 8)]))
      else
        AddMessage(Format('%s references master %d (FormID: %s)',
          [EditorID(e), fileIndex, IntToHex(fixedFormID, 8)]));
    end;
  end;
end;
```

## See Also

- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)
- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)


