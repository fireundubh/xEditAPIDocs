# Signature

## Syntax

```pascal
function Signature(ARecord: IwbMainRecord): string;
```

## Description

Returns the 4-character record type signature.

This function retrieves the Signature property, which identifies the record type (e.g., "WEAP" for weapons, "NPC_" for NPCs, "ARMA" for armor addons). The signature determines which definition template the record uses and what fields it contains. Returns an empty string for invalid records. Signatures are always exactly 4 characters, padded with underscores if needed.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the signature from |

## Returns

Returns the 4-character signature of the record as a string.

## Example

```pascal
// Example 1: Filter records by signature
var
  sig: string;
begin
  if Assigned(e) then begin
    sig := Signature(e);
    if sig = 'WEAP' then
      AddMessage('Found weapon: ' + EditorID(e))
    else if sig = 'ARMO' then
      AddMessage('Found armor: ' + EditorID(e));
  end;
end;

// Example 2: Check if record is a reference (placed object)
var
  sig: string;
begin
  if Assigned(e) then begin
    sig := Signature(e);
    if (sig = 'ACHR') or (sig = 'REFR') then begin
      AddMessage(Name(e) + ' is a placed reference');
      AddMessage('  Base: ' + GetEditValue(ElementByPath(e, 'NAME')));
    end;
  end;
end;

// Example 3: Count records by signature in file
var
  plugin: IwbFile;
  i, count, weaponCount, armorCount: integer;
  rec: IwbMainRecord;
  sig: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    weaponCount := 0;
    armorCount := 0;

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        sig := Signature(rec);
        if sig = 'WEAP' then
          Inc(weaponCount)
        else if sig = 'ARMO' then
          Inc(armorCount);
      end;
    end;

    AddMessage(Format('Weapons: %d, Armor: %d', [weaponCount, armorCount]));
  end;
end;
```

## See Also

- [ChangeFormSignature](IwbMainRecord_ChangeFormSignature.md)
- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)


