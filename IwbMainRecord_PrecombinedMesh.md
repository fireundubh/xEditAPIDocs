# PrecombinedMesh

## Syntax

```pascal
function PrecombinedMesh(ARecord: IwbMainRecord): string;
```

## Description

Returns the precombined mesh path for a Fallout 4 or Fallout 76 placed reference that belongs to a cell precombine.

Supported references include `REFR` and several projectile and hazard types. Placed actors (`ACHR`) are not included. Returns an empty string for other games, other signatures, references that are not precombined, and records that are not main records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The placed reference to look up |

## Returns

Returns the precombined mesh path, or an empty string when the record has none.

## Example

```pascal
// Example 1: Display precombined mesh path
var
  meshPath: string;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if HasPrecombinedMesh(e) then begin
      meshPath := PrecombinedMesh(e);
      AddMessage(Format('%s precombined mesh:', [Name(e)]));
      AddMessage(Format('  %s', [meshPath]));
    end else begin
      AddMessage(Format('%s: No precombined mesh', [Name(e)]));
    end;
  end;
end;

// Example 2: Extract precombined mesh filenames
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k: integer;
  meshPath, fileName: string;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      AddMessage('Precombined mesh files:');

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and HasPrecombinedMesh(refRec) then begin
                  meshPath := PrecombinedMesh(refRec);
                  fileName := ExtractFileName(meshPath);
                  AddMessage(Format('  %s: %s', [Name(refRec), fileName]));
                end;
              end;
            end;
          end;
        end;
      end;
    end;
  end;
end;

// Example 3: Check if precombined mesh file exists
var
  meshPath, fullPath: string;
  dataPath: string;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if HasPrecombinedMesh(e) then begin
      meshPath := PrecombinedMesh(e);
      dataPath := DataPath; // Get game data directory
      if (Length(dataPath) > 0) and (Copy(dataPath, Length(dataPath), 1) <> '\') then
        dataPath := dataPath + '\';
      fullPath := dataPath + meshPath;

      if FileExists(fullPath) then
        AddMessage(Format('%s: Precombined mesh exists', [Name(e)]))
      else
        AddMessage(Format('WARNING: %s: Missing precombined mesh file: %s',
          [Name(e), meshPath]));
    end;
  end;
end;

// Example 4: Group references by precombined mesh
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, idx: integer;
  meshPath: string;
  meshGroups: TStringList;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      meshGroups := TStringList.Create;
      try
        for i := 0 to Pred(ElementCount(childGroup)) do begin
          blockGroup := ElementByIndex(childGroup, i);
          if Assigned(blockGroup) then begin
            for j := 0 to Pred(ElementCount(blockGroup)) do begin
              subBlock := ElementByIndex(blockGroup, j);
              if Assigned(subBlock) then begin
                for k := 0 to Pred(ElementCount(subBlock)) do begin
                  refRec := ElementByIndex(subBlock, k);
                  if Assigned(refRec) and HasPrecombinedMesh(refRec) then begin
                    meshPath := PrecombinedMesh(refRec);
                    idx := meshGroups.IndexOf(meshPath);
                    if idx >= 0 then
                      meshGroups.Objects[idx] := TObject(Integer(meshGroups.Objects[idx]) + 1)
                    else
                      meshGroups.AddObject(meshPath, TObject(1));
                  end;
                end;
              end;
            end;
          end;
        end;

        AddMessage('Precombined meshes usage:');
        for i := 0 to meshGroups.Count - 1 do
          AddMessage(Format('  %s: %d reference(s)',
            [meshGroups[i], Integer(meshGroups.Objects[i])]));
      finally
        meshGroups.Free;
      end;
    end;
  end;
end;
```

## See Also

- [HasPrecombinedMesh](IwbMainRecord_HasPrecombinedMesh.md)


