# SetIsInitiallyDisabled

## Syntax

```pascal
procedure SetIsInitiallyDisabled(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Initially Disabled when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Initially Disabled flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Initially Disabled flag |

## Example

```pascal
// Example 1: Create quest-controlled reference
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    // Make persistent so scripts can access it
    SetIsPersistent(e, true);
    // Start disabled - quest will enable it
    SetIsInitiallyDisabled(e, true);

    AddMessage(Format('%s configured for quest control', [Name(e)]));
    AddMessage('Reference will be disabled until enabled by script');
  end;
end;

// Example 2: Enable initially disabled reference
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if GetIsInitiallyDisabled(e) then begin
      SetIsInitiallyDisabled(e, false);
      AddMessage(Format('%s will now be active when cell loads', [Name(e)]));
    end else begin
      AddMessage(Format('%s is already active', [Name(e)]));
    end;
  end;
end;

// Example 3: Batch disable all references to specific base object
var
  refRec: IwbMainRecord;
  i, count, disabledCount: integer;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    disabledCount := 0;

    AddMessage(Format('Disabling all placed instances of %s...', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      refRec := ReferencedByIndex(e, i);
      if Assigned(refRec) then begin
        sig := Signature(refRec);
        if (sig = 'REFR') or (sig = 'ACHR') then begin
          SetIsInitiallyDisabled(refRec, true);
          Inc(disabledCount);
          AddMessage(Format('  Disabled: %s', [Name(refRec)]));
        end;
      end;
    end;

    AddMessage(Format('Disabled %d instance(s)', [disabledCount]));
  end;
end;

// Example 4: Toggle initially disabled flag
var
  isDisabled: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isDisabled := GetIsInitiallyDisabled(e);

    SetIsInitiallyDisabled(e, not isDisabled);

    if isDisabled then
      AddMessage(Format('%s enabled (will be active on load)', [Name(e)]))
    else
      AddMessage(Format('%s disabled (must be enabled by script)', [Name(e)]));
  end;
end;
```

## See Also

- [GetIsInitiallyDisabled](IwbMainRecord_GetIsInitiallyDisabled.md)
- [SetIsDeleted](IwbMainRecord_SetIsDeleted.md)
- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)
- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


