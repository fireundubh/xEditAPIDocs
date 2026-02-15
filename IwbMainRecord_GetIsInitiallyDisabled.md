# GetIsInitiallyDisabled

## Syntax

```pascal
function GetIsInitiallyDisabled(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Initially Disabled flag set in its record header.

This function retrieves the IsInitiallyDisabled property, which checks a flag bit specific to reference records (REFR, ACHR, etc.). Initially disabled references are inactive when the cell loads but can be enabled by scripts or quests. Returns false for invalid records or non-reference record types. This is primarily used for placed references in the game world.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Initially Disabled flag on |

## Returns

Returns `True` if the record is flagged as Initially Disabled, `False` otherwise.

## Example

```pascal
// Example 1: Check if placed reference is initially disabled
var
  cell: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if GetIsInitiallyDisabled(e) then begin
      cell := GetElementLinksTo(e, 'Cell');
      AddMessage(Format('%s in %s starts disabled',
        [Name(e), EditorID(cell)]));
      AddMessage('Must be enabled by script or quest');
    end else begin
      AddMessage(Format('%s is active when cell loads', [Name(e)]));
    end;
  end;
end;

// Example 2: Find all initially disabled references in a cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, count, disabledCount: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      disabledCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and GetIsInitiallyDisabled(refRec) then begin
                  Inc(disabledCount);
                  AddMessage(Format('  Disabled: %s', [Name(refRec)]));
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Found %d initially disabled references in %s',
        [disabledCount, EditorID(e)]));
    end;
  end;
end;

// Example 3: Check quest-enabled references
var
  isPersistent, isDisabled: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isPersistent := GetIsPersistent(e);
    isDisabled := GetIsInitiallyDisabled(e);

    if isPersistent and isDisabled then
      AddMessage(Format('%s: Persistent + Initially Disabled = Quest-controlled',
        [Name(e)]))
    else if isDisabled then
      AddMessage(Format('%s: Initially Disabled (temporary reference)',
        [Name(e)]))
    else if isPersistent then
      AddMessage(Format('%s: Persistent (always active)', [Name(e)]))
    else
      AddMessage(Format('%s: Normal temporary reference', [Name(e)]));
  end;
end;

// Example 4: List references that can be enabled by scripts
var
  plugin: IwbFile;
  i, count, scriptEnableCount: integer;
  rec: IwbMainRecord;
begin
  plugin := FileByIndex(0);
  if Assigned(plugin) then begin
    count := RecordCount(plugin);
    scriptEnableCount := 0;

    AddMessage('Finding script-enable candidates...');

    for i := 0 to count - 1 do begin
      rec := RecordByIndex(plugin, i);
      if Assigned(rec) then begin
        if ((Signature(rec) = 'REFR') or (Signature(rec) = 'ACHR')) and
           GetIsInitiallyDisabled(rec) and GetIsPersistent(rec) then begin
          Inc(scriptEnableCount);
          AddMessage(Format('  %s', [Name(rec)]));
        end;
      end;
    end;

    AddMessage(Format('Total: %d references can be script-enabled', [scriptEnableCount]));
  end;
end;
```

## See Also

- [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md)
- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md)
- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)
- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)


