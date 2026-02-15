# SetIsVisibleWhenDistant

## Syntax

```pascal
procedure SetIsVisibleWhenDistant(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Flags `ARecord` as Visible When Distant when `AFlag` is `True` and otherwise when `AFlag` is `False`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Visible When Distant flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Visible When Distant flag |

## Example

```pascal
// Example 1: Enable VWD for large reference
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    SetIsVisibleWhenDistant(e, true);
    AddMessage(Format('%s: VWD enabled (visible from distance)', [Name(e)]));
  end;
end;

// Example 2: Batch enable VWD for all trees in cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec, baseRec: IwbMainRecord;
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
                if Assigned(refRec) and (Signature(refRec) = 'REFR') then begin
                  baseRec := BaseRecord(refRec);
                  if Assigned(baseRec) and (Signature(baseRec) = 'TREE') then begin
                    SetIsVisibleWhenDistant(refRec, true);
                    Inc(vwdCount);
                    AddMessage(Format('  Enabled VWD: %s', [Name(refRec)]));
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Enabled VWD on %d tree(s)', [vwdCount]));
    end;
  end;
end;

// Example 3: Toggle VWD flag
var
  isVWD: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    isVWD := GetIsVisibleWhenDistant(e);

    SetIsVisibleWhenDistant(e, not isVWD);

    if isVWD then
      AddMessage(Format('%s: VWD disabled', [Name(e)]))
    else
      AddMessage(Format('%s: VWD enabled', [Name(e)]));
  end;
end;

// Example 4: Enable VWD for large statics based on scale
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec, baseRec: IwbMainRecord;
  i, j, k, enabledCount: integer;
  scale: Single;
  scaleStr: string;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      enabledCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and (Signature(refRec) = 'REFR') then begin
                  baseRec := BaseRecord(refRec);
                  if Assigned(baseRec) and (Signature(baseRec) = 'STAT') then begin
                    scaleStr := GetElementEditValue(refRec, 'XSCL');
                    if scaleStr <> '' then begin
                      scale := StrToFloat(scaleStr);
                      if scale >= 2.0 then begin // Large scaled objects
                        SetIsVisibleWhenDistant(refRec, true);
                        Inc(enabledCount);
                        AddMessage(Format('  Enabled VWD (scale=%f): %s', [scale, Name(refRec)]));
                      end;
                    end;
                  end;
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('Enabled VWD on %d large static(s)', [enabledCount]));
    end;
  end;
end;
```

## See Also

- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)


