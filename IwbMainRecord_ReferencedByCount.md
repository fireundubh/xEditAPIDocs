# ReferencedByCount

## Syntax

```pascal
function ReferencedByCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the count of records that reference this record via FormID fields.

The count includes every record whose FormID fields point at this record. The list is stored on the master, so an override reports the same count as its master. Returns 0 when nothing references the record, when references have not been built, or when `ARecord` is not a main record. [BuildRef](IwbElement_BuildRef.md) on this record rebuilds its outgoing references, not this incoming list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to count incoming references for |

## Returns

Returns the number of records that reference this record as an integer, or 0 when the list is empty or `ARecord` is not a main record.

## Example

```pascal
// Example 1: List all records that reference this record
var
  refByRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    AddMessage(Format('%s is referenced by %d record(s):', [EditorID(e), count]));

    for i := 0 to count - 1 do begin
      refByRec := ReferencedByIndex(e, i);
      if Assigned(refByRec) then
        AddMessage(Format('  [%d] %s (%s)', [i, EditorID(refByRec), Signature(refByRec)]));
    end;
  end;
end;

// Example 2: Find which leveled lists contain an item
var
  leveledListRec: IwbMainRecord;
  i, count: integer;
  sig: string;
begin
  if Assigned(e) then begin
    count := ReferencedByCount(e);
    AddMessage(Format('Checking %d references for leveled lists...', [count]));

    for i := 0 to count - 1 do begin
      leveledListRec := ReferencedByIndex(e, i);
      if Assigned(leveledListRec) then begin
        sig := Signature(leveledListRec);
        if (sig = 'LVLI') or (sig = 'LVLN') then
          AddMessage(Format('  Found in: %s', [EditorID(leveledListRec)]));
      end;
    end;
  end;
end;

// Example 3: Check if record is safe to delete
var
  refCount: integer;
begin
  if Assigned(e) then begin
    refCount := ReferencedByCount(e);

    if refCount = 0 then
      AddMessage(Format('%s: Safe to delete (no references)', [EditorID(e)]))
    else
      AddMessage(Format('%s: WARNING - %d record(s) reference this! Not safe to delete.',
        [EditorID(e), refCount]));
  end;
end;

// Example 4: Find all placed references to a base object
var
  placedRef: IwbMainRecord;
  i, count, refCount: integer;
  sig: string;
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
          AddMessage(Format('  Instance %d: %s', [refCount, Name(placedRef)]));
        end;
      end;
    end;

    AddMessage(Format('Found %d placed instance(s)', [refCount]));
  end;
end;
```

## See Also

- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [BuildRef](IwbElement_BuildRef.md)
- [LinksTo](IwbElement_LinksTo.md)


