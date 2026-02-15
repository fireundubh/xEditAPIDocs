# ChildGroup

## Syntax

```pascal
function ChildGroup(AWorldspace: IwbMainRecord): IwbGroupRecord;
```

## Description

Returns the group contained by `AWorldspace`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AWorldspace | IwbMainRecord | The worldspace or other main record to get the child group from |

## Returns

Returns the IwbGroupRecord contained by the main record.

## Example

```pascal
// Example 1: Iterate through all cells in worldspace
var
  childGroup: IwbGroupRecord;
  i, count: integer;
  cellRec: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'WRLD') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      count := ElementCount(childGroup);
      AddMessage(Format('%s contains %d cell(s):', [EditorID(e), count]));

      for i := 0 to count - 1 do begin
        cellRec := ElementByIndex(childGroup, i);
        if Assigned(cellRec) then
          AddMessage(Format('  [%d] %s', [i, EditorID(cellRec)]));
      end;
    end else begin
      AddMessage(Format('%s has no child group', [EditorID(e)]));
    end;
  end;
end;

// Example 2: Process all placed references in a cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  i, j, k, refCount: integer;
  refRec: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      refCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) then begin
                  Inc(refCount);
                  AddMessage(Format('  Reference %d: %s', [refCount, Name(refRec)]));
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Total references in %s: %d', [EditorID(e), refCount]));
    end;
  end;
end;

// Example 3: Process all topics in a dialogue quest
var
  childGroup: IwbGroupRecord;
  i, count: integer;
  topicRec: IwbMainRecord;
begin
  if Assigned(e) and (Signature(e) = 'DIAL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      count := ElementCount(childGroup);
      AddMessage(Format('%s has %d topic(s):', [EditorID(e), count]));

      for i := 0 to count - 1 do begin
        topicRec := ElementByIndex(childGroup, i);
        if Assigned(topicRec) and (Signature(topicRec) = 'INFO') then
          AddMessage(Format('  Topic %d: %s', [i, EditorID(topicRec)]));
      end;
    end;
  end;
end;

// Example 4: Count child records by type
var
  childGroup: IwbGroupRecord;
  i, count: integer;
  childRec: IwbMainRecord;
  typeCounts: TStringList;
  sig: string;
  idx: integer;
begin
  if Assigned(e) then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      typeCounts := TStringList.Create;
      try
        count := ElementCount(childGroup);

        for i := 0 to count - 1 do begin
          childRec := ElementByIndex(childGroup, i);
          if Assigned(childRec) then begin
            sig := Signature(childRec);
            idx := typeCounts.IndexOf(sig);
            if idx >= 0 then
              typeCounts.Objects[idx] := TObject(Integer(typeCounts.Objects[idx]) + 1)
            else
              typeCounts.AddObject(sig, TObject(1));
          end;
        end;

        AddMessage(Format('Child records in %s:', [EditorID(e)]));
        for i := 0 to typeCounts.Count - 1 do
          AddMessage(Format('  %s: %d', [typeCounts[i], Integer(typeCounts.Objects[i])]));
      finally
        typeCounts.Free;
      end;
    end;
  end;
end;
```

## See Also

- [ChildrenOf](IwbGroupRecord_ChildrenOf.md)
- [FindChildGroup](IwbGroupRecord_FindChildGroup.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)
- [GroupLabel](IwbGroupRecord_GroupLabel.md)
- [GroupType](IwbGroupRecord_GroupType.md)


