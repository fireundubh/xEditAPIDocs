# SetIsPersistent

## Syntax

```pascal
procedure SetIsPersistent(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Persistent when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Persistent flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Persistent flag |

## Example

```pascal
// Example 1: Make reference accessible to scripts
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    SetIsPersistent(e, true);
    AddMessage(Format('%s is now persistent', [Name(e)]));
    AddMessage('Reference will stay loaded and be accessible to scripts');
  end;
end;

// Example 2: Create quest-controlled reference
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    // Make persistent so quest scripts can access it
    SetIsPersistent(e, true);
    // Start disabled - quest will enable when ready
    SetIsInitiallyDisabled(e, true);

    AddMessage(Format('%s configured for quest control:', [Name(e)]));
    AddMessage('  Persistent: Yes (script-accessible)');
    AddMessage('  Initially Disabled: Yes (quest-enabled)');
  end;
end;

// Example 3: Batch make references persistent for script access
var
  refRec: IwbMainRecord;
  i, count, persistentCount: integer;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    persistentCount := 0;

    AddMessage(Format('Making instances of %s persistent...', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      refRec := ReferencedByIndex(e, i);
      if Assigned(refRec) then begin
        sig := Signature(refRec);
        if (sig = 'REFR') or (sig = 'ACHR') then begin
          if not GetIsPersistent(refRec) then begin
            SetIsPersistent(refRec, true);
            Inc(persistentCount);
            AddMessage(Format('  Made persistent: %s', [Name(refRec)]));
          end;
        end;
      end;
    end;

    AddMessage(Format('Set %d reference(s) to persistent', [persistentCount]));
  end;
end;

// Example 4: Toggle persistent flag
var
  isPersistent: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isPersistent := GetIsPersistent(e);

    SetIsPersistent(e, not isPersistent);

    if isPersistent then
      AddMessage(Format('%s: Now temporary (unloads with cell)', [Name(e)]))
    else
      AddMessage(Format('%s: Now persistent (always loaded)', [Name(e)]));
  end;
end;
```

## See Also

- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)


