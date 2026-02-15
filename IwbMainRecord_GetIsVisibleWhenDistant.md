# GetIsVisibleWhenDistant

## Syntax

```pascal
function GetIsVisibleWhenDistant(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Visible When Distant

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Visible When Distant flag on |

## Returns

Returns `True` if the record is flagged as Visible When Distant, `False` otherwise.

## Example

```pascal
// Example 1: Check if reference has VWD flag
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if GetIsVisibleWhenDistant(e) then
      AddMessage(Format('%s is visible when distant (VWD enabled)', [Name(e)]))
    else
      AddMessage(Format('%s only visible when near', [Name(e)]));
  end;
end;

// Example 2: Find all VWD-enabled references in cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, vwdCount: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      vwdCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and GetIsVisibleWhenDistant(refRec) then begin
                  Inc(vwdCount);
                  AddMessage(Format('  VWD: %s', [Name(refRec)]));
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('%s has %d VWD reference(s)', [EditorID(e), vwdCount]));
    end;
  end;
end;

// Example 3: Check VWD for large objects
var
  baseRec: IwbMainRecord;
  isVWD: boolean;
  baseType: string;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isVWD := GetIsVisibleWhenDistant(e);
    baseRec := BaseRecord(e);

    if Assigned(baseRec) then begin
      baseType := Signature(baseRec);
      if (baseType = 'TREE') or (baseType = 'STAT') then begin
        if isVWD then
          AddMessage(Format('%s: Large object with VWD enabled', [Name(e)]))
        else
          AddMessage(Format('%s: Large object WITHOUT VWD (may pop in)', [Name(e)]));
      end;
    end;
  end;
end;

// Example 4: List VWD references by base object type
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec, baseRec: IwbMainRecord;
  i, j, k: integer;
  baseType: string;
  typeCounts: TStringList;
  idx: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      typeCounts := TStringList.Create;
      try
        for i := 0 to Pred(ElementCount(childGroup)) do begin
          blockGroup := ElementByIndex(childGroup, i);
          if Assigned(blockGroup) then begin
            for j := 0 to Pred(ElementCount(blockGroup)) do begin
              subBlock := ElementByIndex(blockGroup, j);
              if Assigned(subBlock) then begin
                for k := 0 to Pred(ElementCount(subBlock)) do begin
                  refRec := ElementByIndex(subBlock, k);
                  if Assigned(refRec) and GetIsVisibleWhenDistant(refRec) then begin
                    baseRec := BaseRecord(refRec);
                    if Assigned(baseRec) then begin
                      baseType := Signature(baseRec);
                      idx := typeCounts.IndexOf(baseType);
                      if idx >= 0 then
                        typeCounts.Objects[idx] := TObject(Integer(typeCounts.Objects[idx]) + 1)
                      else
                        typeCounts.AddObject(baseType, TObject(1));
                    end;
                  end;
                end;
              end;
            end;
          end;
        end;

        AddMessage('VWD references by type:');
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

- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


