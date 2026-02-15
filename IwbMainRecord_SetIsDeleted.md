# SetIsDeleted

## Syntax

```pascal
procedure SetIsDeleted(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Sets or clears the Deleted flag in the record's header.

This function assigns to the IsDeleted property, which modifies a flag bit in the record header. Setting this to true marks the record as deleted (ignored by the game but preserved for reference tracking). Setting to false undeletes the record. The change takes effect immediately in memory but must be saved to persist. Prefer this over Remove when you want to preserve the record structure for dependency tracking.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Deleted flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Deleted flag |

## Example

```pascal
// Example 1: Mark record as deleted instead of removing it
var
  refCount: integer;
begin
  if Assigned(e) then begin
    refCount := ReferencedByCount(e);

    if refCount > 0 then begin
      // Record has references - mark as deleted instead of removing
      SetIsDeleted(e, true);
      AddMessage(Format('%s marked as deleted (%d references preserved)',
        [EditorID(e), refCount]));
    end else begin
      // Safe to actually remove
      AddMessage(Format('%s has no references - safe to remove', [EditorID(e)]));
      Remove(e);
    end;
  end;
end;

// Example 2: Restore deleted record
begin
  if Assigned(e) then begin
    if GetIsDeleted(e) then begin
      SetIsDeleted(e, false);
      AddMessage(Format('%s restored (no longer deleted)', [EditorID(e)]));
    end else begin
      AddMessage(Format('%s is not deleted', [EditorID(e)]));
    end;
  end;
end;

// Example 3: Create deletion override in patch plugin
var
  overrideRec: IwbMainRecord;
  patchFile: IwbFile;
begin
  if Assigned(e) then begin
    patchFile := FileByIndex(0);
    if Assigned(patchFile) then begin
      // Copy record to patch file
      overrideRec := wbCopyElementToFile(e, patchFile, false, true);
      if Assigned(overrideRec) then begin
        // Mark the override as deleted
        SetIsDeleted(overrideRec, true);
        AddMessage(Format('Created deletion override for %s in %s',
          [EditorID(e), GetFileName(patchFile)]));
      end;
    end;
  end;
end;

// Example 4: Toggle deleted status
var
  isDeleted: boolean;
begin
  if Assigned(e) then begin
    isDeleted := GetIsDeleted(e);

    // Toggle the flag
    SetIsDeleted(e, not isDeleted);

    if isDeleted then
      AddMessage(Format('%s restored', [EditorID(e)]))
    else
      AddMessage(Format('%s marked as deleted', [EditorID(e)]));
  end;
end;
```

## See Also

- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md)
- [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md)
- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)
- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


