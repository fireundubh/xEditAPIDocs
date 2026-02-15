# GetIsPersistent

## Syntax

```pascal
function GetIsPersistent(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Persistent flag set in its record header.

This function retrieves the IsPersistent property, which checks a flag bit specific to reference records (REFR, ACHR, etc.). Persistent references remain loaded in memory even when their cell is not active, making them accessible to scripts at all times. Returns false for invalid records or non-reference record types. Essential for references that need to be referenced by scripts or quests from anywhere.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Persistent flag on |

## Returns

Returns `True` if the record is flagged as Persistent, `False` otherwise.

## Example

```pascal
// Example 1: Check if reference is always loaded
var
  cell: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if GetIsPersistent(e) then begin
      cell := GetElementLinksTo(e, 'Cell');
      AddMessage(Format('%s in %s is persistent', [Name(e), EditorID(cell)]));
      AddMessage('This reference stays loaded and can be accessed by scripts');
    end else begin
      AddMessage(Format('%s is temporary (unloads with cell)', [Name(e)]));
    end;
  end;
end;

// Example 2: Find all persistent references in plugin
var
  plugin: IwbFile;
  i, count, persistentCount: integer;
  rec: IwbMainRecord;
  sig: string;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    persistentCount := 0;

    AddMessage('Finding persistent references...');

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        sig := Signature(rec);
        if ((sig = 'REFR') or (sig = 'ACHR')) and GetIsPersistent(rec) then begin
          Inc(persistentCount);
          AddMessage(Format('  %s', [Name(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d persistent reference(s)', [persistentCount]));
  end;
end;

// Example 3: Check reference accessibility for scripts
var
  isPersistent, isDisabled: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isPersistent := GetIsPersistent(e);
    isDisabled := GetIsInitiallyDisabled(e);

    if isPersistent then begin
      AddMessage(Format('%s: Accessible to scripts at all times', [Name(e)]));
      if isDisabled then
        AddMessage('  Starts disabled - quest can enable it')
      else
        AddMessage('  Always active');
    end else begin
      AddMessage(Format('%s: Only accessible when cell is loaded', [Name(e)]));
    end;
  end;
end;

// Example 4: Find quest-critical references
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, questRefCount: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      questRefCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and GetIsPersistent(refRec) then begin
                  Inc(questRefCount);
                  AddMessage(Format('  Persistent: %s', [Name(refRec)]));
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('%s has %d persistent reference(s)',
        [EditorID(e), questRefCount]));
    end;
  end;
end;
```

## See Also

- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)


