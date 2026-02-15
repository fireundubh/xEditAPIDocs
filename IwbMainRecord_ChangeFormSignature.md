# ChangeFormSignature

## Syntax

```pascal
procedure ChangeFormSignature(ARecord: IwbMainRecord; ANewSignature: string);
```

## Description

Changes the signature (record type) of a main record to a new value.

The procedure modifies only the 4-character signature of the record while preserving all other record data. This should be used with caution as changing record signatures can break references and functionality if not done correctly.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to change the signature of |
| ANewSignature | string | The new 4-character signature to assign to the record |

## Example

```pascal
// Example 1: Convert LVLI to LVLN (change list type)
var
  oldSig, newSig: string;
begin
  if Assigned(e) then begin
    oldSig := Signature(e);
    newSig := 'LVLN';

    if oldSig = 'LVLI' then begin
      ChangeFormSignature(e, newSig);
      AddMessage(Format('Changed signature: %s -> %s for %s',
        [oldSig, newSig, EditorID(e)]));
    end else begin
      AddMessage(Format('Cannot convert %s to %s', [oldSig, newSig]));
    end;
  end;
end;

// Example 2: Batch convert record types with validation
var
  plugin: IwbFile;
  i, count, convertedCount: integer;
  rec: IwbMainRecord;
  oldSig, newSig: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    oldSig := 'MISC';
    newSig := 'ALCH';
    count := RecordCount(plugin);
    convertedCount := 0;

    AddMessage(Format('Converting %s records to %s...', [oldSig, newSig]));

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and (Signature(rec) = oldSig) then begin
        try
          ChangeFormSignature(rec, newSig);
          Inc(convertedCount);
          AddMessage(Format('  Converted: %s', [EditorID(rec)]));
        except
          on E: Exception do
            AddMessage(Format('  FAILED: %s - %s', [EditorID(rec), E.Message]));
        end;
      end;
    end;

    AddMessage(Format('Converted %d of %d record(s)', [convertedCount, count]));
  end;
end;

// Example 3: Change signature with safety check
var
  currentSig, targetSig: string;
  refCount: integer;
begin
  if Assigned(e) then begin
    currentSig := Signature(e);
    targetSig := 'WEAP';

    // Check for references before changing
    refCount := ReferencedByCount(e);
    if refCount > 0 then begin
      AddMessage(Format('WARNING: %s is referenced by %d record(s)',
        [EditorID(e), refCount]));
      AddMessage('Changing signature may break references!');
    end;

    ChangeFormSignature(e, targetSig);
    AddMessage(Format('Changed %s from %s to %s',
      [EditorID(e), currentSig, targetSig]));
  end;
end;

// Example 4: Convert with EditorID update
var
  oldSig, newSig: string;
  oldID, newID: string;
begin
  if Assigned(e) then begin
    oldSig := Signature(e);
    newSig := 'ARMO';
    oldID := EditorID(e);

    // Change signature
    ChangeFormSignature(e, newSig);

    // Update EditorID to reflect new type
    newID := StringReplace(oldID, oldSig, newSig, [rfReplaceAll]);
    if newID <> oldID then
      SetEditorID(e, newID);

    AddMessage(Format('Converted: %s (%s) -> %s (%s)',
      [oldID, oldSig, newID, newSig]));
  end;
end;
```

## See Also

- [Signature](IwbMainRecord_Signature.md)
- [FormID](IwbMainRecord_FormID.md)
- [EditorID](IwbMainRecord_EditorID.md)


