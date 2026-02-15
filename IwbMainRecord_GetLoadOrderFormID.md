# GetLoadOrderFormID

## Syntax

```pascal
function GetLoadOrderFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the FormID adjusted for the current runtime load order.

This function retrieves the LoadOrderFormID property and converts it to a Cardinal. The returned value has the file index updated to reflect the current load order position (not the saved file index). This is the FormID the game engine uses at runtime. Returns 0 for invalid records. Use this when you need the FormID that will actually work in the game, especially when load order has changed since the file was saved.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the load order Form ID from |

## Returns

Returns the Form ID relative to the current load order as a Cardinal value.

## Example

```pascal
// Example 1: Get runtime FormID for game scripts
var
  loadOrderFormID: Cardinal;
begin
  if Assigned(e) then begin
    loadOrderFormID := GetLoadOrderFormID(e);
    AddMessage(Format('Runtime FormID: %s', [IntToHex(loadOrderFormID, 8)]));
    AddMessage('Use this FormID in console commands and scripts');
  end;
end;

// Example 2: Compare FormID types for DLC record
var
  fileFormID, loadOrderFormID, fixedFormID: Cardinal;
begin
  if Assigned(e) then begin
    fileFormID := FormID(e);
    loadOrderFormID := GetLoadOrderFormID(e);
    fixedFormID := FixedFormID(e);

    AddMessage(Format('File FormID:       %s (saved in plugin)', [IntToHex(fileFormID, 8)]));
    AddMessage(Format('Load Order FormID: %s (current runtime)', [IntToHex(loadOrderFormID, 8)]));
    AddMessage(Format('Fixed FormID:      %s (master-relative)', [IntToHex(fixedFormID, 8)]));
  end;
end;

// Example 3: Build console command with runtime FormID
var
  loadOrderFormID: Cardinal;
  consoleCmd: string;
begin
  if Assigned(e) then begin
    loadOrderFormID := GetLoadOrderFormID(e);
    consoleCmd := Format('player.additem %s 1', [IntToHex(loadOrderFormID, 8)]);
    AddMessage('Console command: ' + consoleCmd);
  end;
end;

// Example 4: Find record by runtime FormID across all files
var
  targetFormID: Cardinal;
  foundRec: IwbMainRecord;
  i: integer;
  plugin: IwbFile;
begin
  targetFormID := $06022DC0; // Runtime FormID to find

  for i := 0 to Pred(FileCount) do begin
    plugin := FileByIndex(i);
    if Assigned(plugin) then begin
      foundRec := RecordByFormID(plugin, targetFormID, true);
      if Assigned(foundRec) then begin
        AddMessage(Format('Found: %s in %s', [EditorID(foundRec), GetFileName(plugin)]));
        Break;
      end;
    end;
  end;
end;
```

## See Also

- [FileFormIDtoLoadOrderFormID](IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [LoadOrderFormIDtoFileFormID](IwbFile_LoadOrderFormIDtoFileFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


