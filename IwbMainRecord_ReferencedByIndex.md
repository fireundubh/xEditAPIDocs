# ReferencedByIndex

## Syntax

```pascal
function ReferencedByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns the record at the specified index in the list of records referencing this record.

This function accesses the ReferencedBy property by index, providing array-style access to all records that contain FormID fields pointing to this record. The order is determined internally and may not be meaningful. Use ReferencedByCount to get the valid index range. Returns nil for invalid indices. Ensure BuildRef has been called to populate the reference tracking.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get incoming references from |
| AIndex | integer | The zero-based index in the array of referencing records |

## Returns

Returns the IwbMainRecord at the specified index that references this record.

## Example

```pascal
// Example 1: Find all placed references of a base object
var
  placedRef: IwbMainRecord;
  i, count, refCount: integer;
  sig: string;
  cell: IwbMainRecord;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    refCount := 0;

    AddMessage(Format('Finding placed instances of %s...', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      placedRef := ReferencedByIndex(e, i);
      if Assigned(placedRef) then begin
        sig := Signature(placedRef);
        if (sig = 'REFR') or (sig = 'ACHR') then begin
          Inc(refCount);
          cell := GetElementLinksTo(placedRef, 'Cell');
          if Assigned(cell) then
            AddMessage(Format('  Instance %d: %s in cell %s',
              [refCount, Name(placedRef), EditorID(cell)]));
        end;
      end;
    end;

    AddMessage(Format('Total: %d placed instance(s)', [refCount]));
  end;
end;

// Example 2: Find which leveled lists include an item
var
  leveledListRec: IwbMainRecord;
  i, count: integer;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    AddMessage(Format('%s appears in these leveled lists:', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      leveledListRec := ReferencedByIndex(e, i);
      if Assigned(leveledListRec) then begin
        sig := Signature(leveledListRec);
        if (sig = 'LVLI') or (sig = 'LVLN') or (sig = 'LVSP') then
          AddMessage(Format('  %s (%s)', [EditorID(leveledListRec), sig]));
      end;
    end;
  end;
end;

// Example 3: Check dependencies before deleting record
var
  refByRec: IwbMainRecord;
  i, count: integer;
  dependencies: TStringList;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);

    if count = 0 then begin
      AddMessage(Format('%s: Safe to delete (no references)', [EditorID(e)]));
    end else begin
      dependencies := TStringList.Create;
      try
        for i := 0 to count - 1 do begin
          refByRec := ReferencedByIndex(e, i);
          if Assigned(refByRec) then begin
            sig := Signature(refByRec);
            dependencies.Add(Format('  %s (%s) in %s',
              [EditorID(refByRec), sig, GetFileName(GetFile(refByRec))]));
          end;
        end;

        AddMessage(Format('WARNING: Cannot delete %s - %d dependencies:',
          [EditorID(e), count]));
        for i := 0 to dependencies.Count - 1 do
          AddMessage(dependencies[i]);
      finally
        dependencies.Free;
      end;
    end;
  end;
end;

// Example 4: Update all references after changing a FormID
var
  refByRec: IwbMainRecord;
  oldFormID, newFormID: Cardinal;
  i, count, updateCount: integer;
begin
  if Assigned(e) then begin
    oldFormID := GetLoadOrderFormID(e);
    newFormID := GetNewFormID(GetFile(e));

    count := ReferencedByCount(e);
    updateCount := 0;

    AddMessage(Format('Updating %d references from %s to %s...',
      [count, IntToHex(oldFormID, 8), IntToHex(newFormID, 8)]));

    for i := 0 to count - 1 do begin
      refByRec := ReferencedByIndex(e, i);
      if Assigned(refByRec) then begin
        if CompareExchangeFormID(refByRec, oldFormID, newFormID) then begin
          Inc(updateCount);
          AddMessage(Format('  Updated: %s', [EditorID(refByRec)]));
        end;
      end;
    end;

    AddMessage(Format('Successfully updated %d of %d references', [updateCount, count]));
    SetLoadOrderFormID(e, newFormID);
  end;
end;
```

## See Also

- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [BuildRef](IwbElement_BuildRef.md)
- [LinksTo](IwbElement_LinksTo.md)


