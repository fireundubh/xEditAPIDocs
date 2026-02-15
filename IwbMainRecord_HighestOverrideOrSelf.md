# HighestOverrideOrSelf

## Syntax

```pascal
function HighestOverrideOrSelf(ARecord: IwbMainRecord; AMaxLoadOrder: integer): IwbMainRecord;
```

## Description

Returns an overriding record for `ARecord` that loads last nearest to `AMaxLoadOrder`, or the record itself

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to find the highest override for |
| AMaxLoadOrder | integer | The maximum load order to search up to |

## Returns

Returns the highest override record up to the specified load order, or the record itself if no override exists.

## Example

```pascal
// Example 1: Get record version as of specific plugin in load order
var
  contextRec: IwbMainRecord;
  contextFile: IwbFile;
  maxLoadOrder: integer;
begin
  if Assigned(e) then begin
    contextFile := FileByIndex(5); // Check state as of 6th plugin
    if Assigned(contextFile) then begin
      maxLoadOrder := GetLoadOrder(contextFile);
      contextRec := HighestOverrideOrSelf(e, maxLoadOrder);

      if Assigned(contextRec) then
        AddMessage(Format('As of %s: record version from %s',
          [GetFileName(contextFile), GetFileName(GetFile(contextRec))]));
    end;
  end;
end;

// Example 2: Compare record state at different load order points
var
  beforeRec, afterRec: IwbMainRecord;
  beforeValue, afterValue: string;
  beforeLoadOrder, afterLoadOrder: integer;
begin
  if Assigned(e) then begin
    beforeLoadOrder := 10;
    afterLoadOrder := 20;

    beforeRec := HighestOverrideOrSelf(e, beforeLoadOrder);
    afterRec := HighestOverrideOrSelf(e, afterLoadOrder);

    if Assigned(beforeRec) and Assigned(afterRec) then begin
      beforeValue := GetElementEditValue(beforeRec, 'DATA\Value');
      afterValue := GetElementEditValue(afterRec, 'DATA\Value');

      AddMessage(Format('Value at LO %d: %s', [beforeLoadOrder, beforeValue]));
      AddMessage(Format('Value at LO %d: %s', [afterLoadOrder, afterValue]));
    end;
  end;
end;

// Example 3: Find which plugins modify a record up to current plugin
var
  highestRec: IwbMainRecord;
  currentFile: IwbFile;
  currentLoadOrder: integer;
begin
  if Assigned(e) then begin
    currentFile := GetFile(e);
    if Assigned(currentFile) then begin
      currentLoadOrder := GetLoadOrder(currentFile);
      highestRec := HighestOverrideOrSelf(e, currentLoadOrder);

      if Assigned(highestRec) then begin
        if Equals(e, highestRec) then
          AddMessage('Record is the highest override up to this point')
        else
          AddMessage(Format('Overridden by: %s',
            [GetFileName(GetFile(highestRec))]));
      end;
    end;
  end;
end;

// Example 4: Build override timeline showing when record changed
var
  masterRec, overrideRec, prevRec: IwbMainRecord;
  i, count: integer;
  fileLoadOrder: integer;
  timeline: string;
begin
  masterRec := MasterOrSelf(e);
  if Assigned(masterRec) then begin
    count := OverrideCount(masterRec);
    timeline := Format('FormID %s timeline:', [IntToHex(GetLoadOrderFormID(masterRec), 8)]);

    for i := 0 to count - 1 do begin
      overrideRec := OverrideByIndex(masterRec, i);
      if Assigned(overrideRec) then begin
        fileLoadOrder := GetLoadOrder(GetFile(overrideRec));
        prevRec := HighestOverrideOrSelf(masterRec, fileLoadOrder - 1);

        timeline := timeline + Format(#13#10'  [%d] %s',
          [fileLoadOrder, GetFileName(GetFile(overrideRec))]);
      end;
    end;

    AddMessage(timeline);
  end;
end;
```

## See Also

- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
- [OverrideByIndex](IwbMainRecord_OverrideByIndex.md)


