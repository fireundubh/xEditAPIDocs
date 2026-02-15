# HasPrecombinedMesh

## Syntax

```pascal
function HasPrecombinedMesh(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is a Fallout 4 reference that has precombined mesh data

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The reference record to check for precombined mesh data |

## Returns

Returns `True` if the record has precombined mesh data, `False` otherwise.

## Example

```pascal
// Example 1: Check if reference uses precombined meshes
var
  meshPath: string;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    if HasPrecombinedMesh(e) then begin
      meshPath := PrecombinedMesh(e);
      AddMessage(Format('%s uses precombined mesh:', [Name(e)]));
      AddMessage(Format('  Path: %s', [meshPath]));
    end else begin
      AddMessage(Format('%s: No precombined mesh', [Name(e)]));
    end;
  end;
end;

// Example 2: Find all references with precombined meshes in cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k, precomCount: integer;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      precomCount := 0;

      for i := 0 to Pred(ElementCount(childGroup)) do begin
        blockGroup := ElementByIndex(childGroup, i);
        if Assigned(blockGroup) then begin
          for j := 0 to Pred(ElementCount(blockGroup)) do begin
            subBlock := ElementByIndex(blockGroup, j);
            if Assigned(subBlock) then begin
              for k := 0 to Pred(ElementCount(subBlock)) do begin
                refRec := ElementByIndex(subBlock, k);
                if Assigned(refRec) and HasPrecombinedMesh(refRec) then begin
                  Inc(precomCount);
                  AddMessage(Format('  Precombined: %s', [Name(refRec)]));
                end;
              end;
            end;
          end;
        end;
      end;

      AddMessage(Format('%s: %d reference(s) with precombined meshes',
        [EditorID(e), precomCount]));
    end;
  end;
end;

// Example 3: Check for precombined mesh conflicts
var
  hasPrecombined, isDeleted: boolean;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    hasPrecombined := HasPrecombinedMesh(e);
    isDeleted := GetIsDeleted(e);

    if hasPrecombined and isDeleted then
      AddMessage(Format('WARNING: %s is deleted but has precombined mesh data',
        [Name(e)]))
    else if hasPrecombined then
      AddMessage(Format('%s: Uses precombined mesh (optimization active)', [Name(e)]));
  end;
end;

// Example 4: List unique precombined mesh paths in cell
var
  childGroup, blockGroup, subBlock: IwbContainer;
  refRec: IwbMainRecord;
  i, j, k: integer;
  meshPaths: TStringList;
  meshPath: string;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      meshPaths := TStringList.Create;
      try
        meshPaths.Sorted := true;
        meshPaths.Duplicates := dupIgnore;

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
                    if meshPath <> '' then
                      meshPaths.Add(meshPath);
                  end;
                end;
              end;
            end;
          end;
        end;

        AddMessage(Format('Unique precombined meshes in %s:', [EditorID(e)]));
        for i := 0 to meshPaths.Count - 1 do
          AddMessage(Format('  %s', [meshPaths[i]]));
      finally
        meshPaths.Free;
      end;
    end;
  end;
end;
```

## See Also

- [PrecombinedMesh](IwbMainRecord_PrecombinedMesh.md)


