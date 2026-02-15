# ReferencesCount

## Syntax

```pascal
function ReferencesCount(ARecord: IwbMainRecord): integer;
```

## Description

Returns the number of records linked to by `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to count outgoing references for |

## Returns

Returns the number of records this record references as an integer.

## Example

```pascal
// Example 1: List all records referenced by this record
var
  refRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    count := ReferencesCount(e);
    AddMessage(Format('%s references %d record(s):', [EditorID(e), count]));

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then
        AddMessage(Format('  [%d] %s (%s)', [i, EditorID(refRec), Signature(refRec)]));
    end;
  end;
end;

// Example 2: Find all dependencies for a placed reference
var
  refRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    count := ReferencesCount(e);
    AddMessage(Format('%s has %d dependencies:', [Name(e), count]));

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then begin
        AddMessage(Format('  %s: %s (%s)',
          [Signature(refRec), EditorID(refRec), GetFileName(GetFile(refRec))]));
      end;
    end;
  end;
end;

// Example 3: Check if record has any dependencies
var
  refCount: integer;
begin
  if Assigned(e) then begin
    refCount := ReferencesCount(e);

    if refCount = 0 then
      AddMessage(Format('%s: No dependencies (standalone record)', [EditorID(e)]))
    else
      AddMessage(Format('%s: Has %d dependencies', [EditorID(e), refCount]));
  end;
end;

// Example 4: Copy all referenced records to new plugin
var
  refRec, copiedRec: IwbMainRecord;
  targetFile: IwbFile;
  i, count, copiedCount: integer;
begin
  if Assigned(e) then begin
    targetFile := FileByIndex(0);
    if Assigned(targetFile) then begin
      count := ReferencesCount(e);
      copiedCount := 0;

      AddMessage(Format('Copying %d dependencies to %s...',
        [count, GetFileName(targetFile)]));

      for i := 0 to count - 1 do begin
        refRec := ReferencesByIndex(e, i);
        if Assigned(refRec) then begin
          copiedRec := wbCopyElementToFile(refRec, targetFile, false, true);
          if Assigned(copiedRec) then begin
            Inc(copiedCount);
            AddMessage(Format('  Copied: %s', [EditorID(refRec)]));
          end;
        end;
      end;

      AddMessage(Format('Copied %d of %d dependencies', [copiedCount, count]));
    end;
  end;
end;
```

## See Also

- [ReferencesByIndex](IwbMainRecord_ReferencesByIndex.md)
- [ReferencedByCount](IwbMainRecord_ReferencedByCount.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)
- [BuildRef](IwbElement_BuildRef.md)


