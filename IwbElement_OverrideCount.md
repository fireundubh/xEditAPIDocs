# OverrideCount (IwbElement)

## Syntax

```pascal
function OverrideCount(AElement: IwbElement): integer;
```

## Description

Returns the number of override records for this element.

For master records, this function returns the number of override records that exist in other plugins. Returns 0 for elements that are not master records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the override count for |

## Returns

Returns the number of override records as an integer.

## Example

```pascal
// Example 1: Check for overrides
var
  overrideCount: integer;
begin
  if Assigned(e) then begin
    overrideCount := OverrideCount(e);
    if overrideCount > 0 then
      AddMessage(Format('%s has %d override(s)', [EditorID(e), overrideCount]))
    else
      AddMessage(Format('%s has no overrides', [EditorID(e)]));
  end;
end;

// Example 2: Find highly modified records
var
  rec: IwbMainRecord;
  count: integer;
  i: integer;
  highModCount: integer;
begin
  highModCount := 0;
  for i := 0 to RecordCount - 1 do begin
    rec := RecordByIndex(i);
    if Assigned(rec) then begin
      count := OverrideCount(rec);
      if count >= 5 then begin
        Inc(highModCount);
        AddMessage(Format('%s: %d overrides', [EditorID(rec), count]));
      end;
    end;
  end;
  AddMessage(Format('Found %d records with 5+ overrides', [highModCount]));
end;

// Example 3: Report override distribution
var
  rec: IwbMainRecord;
  count: integer;
  i: integer;
  noOverrides, fewOverrides, manyOverrides: integer;
begin
  noOverrides := 0;
  fewOverrides := 0;
  manyOverrides := 0;

  for i := 0 to RecordCount - 1 do begin
    rec := RecordByIndex(i);
    if Assigned(rec) and IsMaster(rec) then begin
      count := OverrideCount(rec);
      if count = 0 then
        Inc(noOverrides)
      else if count <= 3 then
        Inc(fewOverrides)
      else
        Inc(manyOverrides);
    end;
  end;

  AddMessage('Override distribution:');
  AddMessage(Format('  No overrides: %d', [noOverrides]));
  AddMessage(Format('  1-3 overrides: %d', [fewOverrides]));
  AddMessage(Format('  4+ overrides: %d', [manyOverrides]));
end;
```

## See Also

- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [IsMaster](IwbMainRecord_IsMaster.md)


