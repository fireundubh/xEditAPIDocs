# SetLoadOrderFormID

## Syntax

```pascal
procedure SetLoadOrderFormID(ARecord: IwbMainRecord; ALoadOrderFormID: Cardinal);
```

## Description

Changes the record's FormID to a new value specified in load order format.

This function assigns to the LoadOrderFormID property, converting the load order FormID to file-local format before storing. The upper byte of the FormID determines the owning file. Changing an override's FormID to use the current file's index converts it to a new master record. Changing any record's FormID to use another file's index makes it an injected record. Raises an exception if the new FormID already exists or cannot be mapped to a valid master.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to change the Form ID on |
| ALoadOrderFormID | Cardinal | The new load order Form ID to assign |

## Example

```pascal
// Example 1: Assign new FormID to copied record
var
  copiedRec: IwbMainRecord;
  targetFile: IwbFile;
  newFormID: Cardinal;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(0);
    if Assigned(targetFile) then begin
      copiedRec := wbCopyElementToFile(e, targetFile, false, true);
      if Assigned(copiedRec) then begin
        newFormID := GetNewFormID(targetFile);
        SetLoadOrderFormID(copiedRec, newFormID);
        AddMessage(Format('Assigned new FormID: %s', [IntToHex(newFormID, 8)]));
      end;
    end;
  end;
end;

// Example 2: Change FormID file index to current plugin
var
  currentFile: IwbFile;
  currentFormID, newFormID: Cardinal;
  loadOrder: byte;
begin
  if Assigned(e) then begin
    currentFile := GetFile(e);
    if Assigned(currentFile) then begin
      currentFormID := GetLoadOrderFormID(e);
      loadOrder := GetLoadOrder(currentFile);
      newFormID := (currentFormID and $00FFFFFF) or (loadOrder shl 24);

      SetLoadOrderFormID(e, newFormID);
      AddMessage(Format('Changed FormID from %s to %s',
        [IntToHex(currentFormID, 8), IntToHex(newFormID, 8)]));
    end;
  end;
end;

// Example 3: Update all references after changing FormID
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
  i, refCount: integer;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newFormID := GetNewFormID(GetFile(e));

    // Update all records that reference this one
    refCount := ReferencedByCount(e);
    for i := 0 to refCount - 1 do begin
      refByRec := ReferencedByIndex(e, i);
      if Assigned(refByRec) then
        CompareExchangeFormID(refByRec, oldFormID, newFormID);
    end;

    // Now change the record's FormID
    SetLoadOrderFormID(e, newFormID);
    AddMessage(Format('Updated FormID and %d references', [refCount]));
  end;
end;
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)


