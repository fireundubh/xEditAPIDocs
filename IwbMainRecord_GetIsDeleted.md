# GetIsDeleted

## Syntax

```pascal
function GetIsDeleted(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Deleted flag set in its record header.

This function retrieves the IsDeleted property, which checks a flag bit in the record's header flags field. Deleted records are typically ignored by the game engine but remain in the file for reference tracking. Returns false for invalid records. This is a header flag, distinct from actually removing the record from the file. Commonly used to mark records as removed without breaking references.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Deleted flag on |

## Returns

Returns `True` if the record is flagged as Deleted, `False` otherwise.

## Example

```pascal
// Example 1: Filter out deleted records
var
  plugin: IwbFile;
  i, count, activeCount: integer;
  rec: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    activeCount := 0;

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and not GetIsDeleted(rec) then begin
        Inc(activeCount);
        AddMessage(Format('Active: %s', [EditorID(rec)]));
      end;
    end;

    AddMessage(Format('Found %d active records (out of %d total)', [activeCount, count]));
  end;
end;

// Example 2: Check deleted status before processing
begin
  if Assigned(e) then begin
    if GetIsDeleted(e) then begin
      AddMessage(Format('WARNING: %s is flagged as deleted', [EditorID(e)]));
      AddMessage('This record is ignored by the game');
    end else begin
      AddMessage(Format('%s is active', [EditorID(e)]));
      // Safe to process...
    end;
  end;
end;

// Example 3: Find all deleted records in plugin
var
  plugin: IwbFile;
  i, count, deletedCount: integer;
  rec: IwbMainRecord;
  deletedList: TStringList;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    deletedList := TStringList.Create;
    try
      count := RecordCount(plugin);
      deletedCount := 0;

      for i := 0 to count - 1 do begin
        rec := RecordByIndex(plugin, i);
        if Assigned(rec) and GetIsDeleted(rec) then begin
          Inc(deletedCount);
          deletedList.Add(Format('%s (%s)', [EditorID(rec), Signature(rec)]));
        end;
      end;

      AddMessage(Format('Found %d deleted record(s) in %s:',
        [deletedCount, GetFileName(plugin)]));
      for i := 0 to deletedList.Count - 1 do
        AddMessage('  ' + deletedList[i]);
    finally
      deletedList.Free;
    end;
  end;
end;

// Example 4: Warn when editing deleted override
var
  masterRec: IwbMainRecord;
begin
  if Assigned(e) then begin
    if GetIsDeleted(e) then begin
      if IsMaster(e) then
        AddMessage('Record is deleted in master file')
      else begin
        masterRec := Master(e);
        if Assigned(masterRec) and GetIsDeleted(masterRec) then
          AddMessage('WARNING: Overriding a deleted master record')
        else
          AddMessage('This override marks the record as deleted');
      end;
    end;
  end;
end;
```

## See Also

- [SetIsDeleted](IwbMainRecord_SetIsDeleted.md)
- [GetIsInitiallyDisabled](IwbMainRecord_GetIsInitiallyDisabled.md)
- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)
- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)


