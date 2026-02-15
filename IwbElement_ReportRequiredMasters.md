# ReportRequiredMasters

## Syntax

```pascal
procedure ReportRequiredMasters(AElement: IwbElement; AListOut: TStrings; AAsNew: boolean; ARecursive: boolean);
```

## Description

Checks which master files an element depends on and adds their filenames to the output list.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to check for required masters |
| AListOut | TStrings | The string list to store the required master filenames |
| AAsNew | boolean | Boolean parameter for checking as new |
| ARecursive | boolean | If true, checks children elements of containers |

## Example

```pascal
// Example 1: Get required masters for record
var
  masters: TStringList;
  i: integer;
begin
  if Assigned(e) then begin
    masters := TStringList.Create;
    try
      ReportRequiredMasters(e, masters, False, True);
      if masters.Count > 0 then begin
        AddMessage(Format('%s requires %d master(s):', [EditorID(e), masters.Count]));
        for i := 0 to masters.Count - 1 do
          AddMessage('  ' + masters[i]);
      end else
        AddMessage(Format('%s has no master dependencies', [EditorID(e)]));
    finally
      masters.Free;
    end;
  end;
end;

// Example 2: Check masters before copying
var
  targetFile: IwbFile;
  masters: TStringList;
  i: integer;
  canCopy: boolean;
begin
  targetFile := FileByIndex(FileCount - 1);
  if Assigned(e) and Assigned(targetFile) then begin
    masters := TStringList.Create;
    try
      ReportRequiredMasters(e, masters, True, True);
      canCopy := True;

      // Check if target file has all required masters
      for i := 0 to masters.Count - 1 do begin
        if not HasMaster(targetFile, masters[i]) then begin
          AddMessage(Format('ERROR: %s requires missing master: %s',
            [EditorID(e), masters[i]]));
          canCopy := False;
        end;
      end;

      if canCopy then begin
        wbCopyElementToFile(e, targetFile, False, True);
        AddMessage(Format('Copied %s to %s', [EditorID(e), GetFileName(targetFile)]));
      end;
    finally
      masters.Free;
    end;
  end;
end;

// Example 3: Analyze master dependencies for file
var
  pluginFile: IwbFile;
  i, j: integer;
  rec: IwbMainRecord;
  masters: TStringList;
  allMasters: TStringList;
begin
  pluginFile := FileByIndex(0);
  if Assigned(pluginFile) then begin
    allMasters := TStringList.Create;
    masters := TStringList.Create;
    try
      allMasters.Sorted := True;
      allMasters.Duplicates := dupIgnore;

      for i := 0 to RecordCount(pluginFile) - 1 do begin
        rec := RecordByIndex(pluginFile, i);
        if Assigned(rec) then begin
          masters.Clear;
          ReportRequiredMasters(rec, masters, False, True);
          for j := 0 to masters.Count - 1 do
            allMasters.Add(masters[j]);
        end;
      end;

      AddMessage(Format('%s total master dependencies:', [GetFileName(pluginFile)]));
      for i := 0 to allMasters.Count - 1 do
        AddMessage('  ' + allMasters[i]);
    finally
      masters.Free;
      allMasters.Free;
    end;
  end;
end;
```

## See Also

- [HasMaster](IwbFile_HasMaster.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)


