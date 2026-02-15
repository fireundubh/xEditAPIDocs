# ReferencesByIndex

## Syntax

```pascal
function ReferencesByIndex(ARecord: IwbMainRecord; AIndex: integer): IwbMainRecord;
```

## Description

Returns record at `AIndex` in array of records linked to by `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get outgoing references from |
| AIndex | integer | The zero-based index in the array of referenced records |

## Returns

Returns the IwbMainRecord at the specified index that this record references.

## Example

```pascal
// Example 1: List all outgoing references with field paths
var
  refRec: IwbMainRecord;
  i, count: integer;
begin
  if Assigned(e) then begin
    count := ReferencesCount(e);
    AddMessage(Format('%s references these records:', [EditorID(e)]));

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then
        AddMessage(Format('  [%d] %s (%s) from %s',
          [i, EditorID(refRec), Signature(refRec), GetFileName(GetFile(refRec))]));
    end;
  end;
end;

// Example 2: Find base object of placed reference
var
  i, count: integer;
  refRec: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    count := ReferencesCount(e);

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then begin
        // Check for common base object signatures
        if (Signature(refRec) = 'STAT') or
           (Signature(refRec) = 'WEAP') or
           (Signature(refRec) = 'ARMO') or
           (Signature(refRec) = 'MISC') then begin
          AddMessage(Format('Base object: %s (%s)',
            [EditorID(refRec), Signature(refRec)]));
        end;
      end;
    end;
  end;
end;

// Example 3: Check for missing master dependencies
var
  refRec: IwbMainRecord;
  recFile, refFile: IwbFile;
  i, count, missingCount: integer;
begin
  if Assigned(e) then begin
    recFile := GetFile(e);
    count := ReferencesCount(e);
    missingCount := 0;

    AddMessage(Format('Checking %d dependencies for %s...', [count, EditorID(e)]));

    for i := 0 to count - 1 do begin
      refRec := ReferencesByIndex(e, i);
      if Assigned(refRec) then begin
        refFile := GetFile(refRec);
        if Assigned(refFile) and (refFile <> recFile) then begin
          // Check if reference file is in current file's masters
          if IndexOfMaster(recFile, GetFileName(refFile)) = -1 then begin
            Inc(missingCount);
            AddMessage(Format('  MISSING MASTER: %s needs %s',
              [EditorID(refRec), GetFileName(refFile)]));
          end;
        end;
      end;
    end;

    if missingCount > 0 then
      AddMessage(Format('WARNING: %d missing master(s) detected', [missingCount]));
  end;
end;

// Example 4: Build dependency graph for complex record
var
  refRec: IwbMainRecord;
  i, count: integer;
  graph: TStringList;
  indent: string;
begin
  if Assigned(e) then begin
    graph := TStringList.Create;
    try
      graph.Add(Format('Dependency graph for %s:', [EditorID(e)]));
      count := ReferencesCount(e);

      for i := 0 to count - 1 do begin
        refRec := ReferencesByIndex(e, i);
        if Assigned(refRec) then begin
          indent := '  ';
          graph.Add(Format('%s|- %s (%s)',
            [indent, EditorID(refRec), Signature(refRec)]));

          // Could recursively show nested dependencies
          if ReferencesCount(refRec) > 0 then
            graph.Add(Format('%s   (has %d sub-dependencies)',
              [indent, ReferencesCount(refRec)]));
        end;
      end;

      for i := 0 to graph.Count - 1 do
        AddMessage(graph[i]);
    finally
      graph.Free;
    end;
  end;
end;
```

## See Also

- [ReferencesCount](IwbMainRecord_ReferencesCount.md)
- [ReferencedByIndex](IwbMainRecord_ReferencedByIndex.md)
- [UpdateRefs](IwbMainRecord_UpdateRefs.md)
- [LinksTo](IwbElement_LinksTo.md)


