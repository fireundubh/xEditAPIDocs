# SetEditorID

## Syntax

```pascal
procedure SetEditorID(ARecord: IwbMainRecord; AEditorID: string);
```

## Description

Sets the Editor ID of the record to the specified string value.

If the record definition has an Editor ID member and that subrecord is missing, it is created. If the record cannot have an Editor ID, the call does nothing. A value equal to the current Editor ID is left unchanged.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Editor ID on |
| AEditorID | string | The new Editor ID value to assign |

## Returns

Returns nothing.

## Example

```pascal
// Example 1: Rename record with validation
var
  currentID, newID: string;
begin
  if Assigned(e) then begin
    currentID := EditorID(e);
    newID := 'MyCustomWeapon01';

    if currentID <> newID then begin
      SetEditorID(e, newID);
      AddMessage(Format('Renamed: %s -> %s', [currentID, newID]));
    end else begin
      AddMessage('EditorID already set to: ' + newID);
    end;
  end;
end;

// Example 2: Add prefix to all records of specific type
var
  plugin: IwbFile;
  i, count, renamedCount: integer;
  rec: IwbMainRecord;
  oldID, newID: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    renamedCount := 0;

    AddMessage('Adding "Custom_" prefix to all weapons...');

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) and (Signature(rec) = 'WEAP') then begin
        oldID := EditorID(rec);
        if (oldID <> '') and (Pos('Custom_', oldID) <> 1) then begin
          newID := 'Custom_' + oldID;
          SetEditorID(rec, newID);
          Inc(renamedCount);
          AddMessage(Format('  %s -> %s', [oldID, newID]));
        end;
      end;
    end;

    AddMessage(Format('Renamed %d weapon(s)', [renamedCount]));
  end;
end;

// Example 3: Generate unique EditorID based on FormID
var
  formID: Cardinal;
  newID: string;
begin
  if Assigned(e) then begin
    formID := GetLoadOrderFormID(e);
    newID := Format('Auto_%s_%s', [Signature(e), IntToHex(formID, 8)]);

    SetEditorID(e, newID);
    AddMessage(Format('Generated EditorID: %s', [newID]));
  end;
end;

// Example 4: Ensure EditorID matches naming convention
var
  currentID, expectedID: string;
  sig: string;
begin
  if Assigned(e) then begin
    sig := Signature(e);
    currentID := EditorID(e);

    // Enforce naming convention: <Type>_<Name>
    if (currentID <> '') and (Pos(sig + '_', currentID) <> 1) then begin
      expectedID := sig + '_' + currentID;
      SetEditorID(e, expectedID);
      AddMessage(Format('Fixed naming: %s -> %s', [currentID, expectedID]));
    end else begin
      AddMessage('EditorID follows naming convention: ' + currentID);
    end;
  end;
end;
```

## See Also

- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)
- [Signature](IwbMainRecord_Signature.md)


