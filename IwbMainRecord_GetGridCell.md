# GetGridCell

## Syntax

```pascal
function GetGridCell(ARecord: IwbMainRecord): TwbGridCell;
```

## Description

Returns a `TwbGridCell` object containing the `X` and `Y` coordinates for `ARecord` (must be an exterior cell record)

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The exterior cell record to get grid coordinates from |

## Returns

Returns a TwbGridCell object with X and Y coordinates.

## Example

```pascal
// Example 1: Display exterior cell coordinates
var
  grid: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    grid := GetGridCell(e);
    AddMessage(Format('%s is at grid coordinates:', [EditorID(e)]));
    AddMessage(Format('  X: %d', [grid.x]));
    AddMessage(Format('  Y: %d', [grid.y]));
    AddMessage(Format('Grid label: (%d, %d)', [grid.x, grid.y]));
  end;
end;

// Example 2: Find cells in specific grid area
var
  childGroup: IwbContainer;
  i, count, foundCount: integer;
  cellRec: IwbMainRecord;
  grid: TwbGridCell;
  minX, maxX, minY, maxY: integer;
begin
  if Assigned(e) and (Signature(e) = 'WRLD') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      minX := -10;
      maxX := 10;
      minY := -10;
      maxY := 10;
      foundCount := 0;

      AddMessage(Format('Finding cells in grid area (%d,%d) to (%d,%d)...',
        [minX, minY, maxX, maxY]));

      count := ElementCount(childGroup);
      for i := 0 to count - 1 do begin
        cellRec := ElementByIndex(childGroup, i);
        if Assigned(cellRec) and (Signature(cellRec) = 'CELL') then begin
          grid := GetGridCell(cellRec);
          if (grid.x >= minX) and (grid.x <= maxX) and
             (grid.y >= minY) and (grid.y <= maxY) then begin
            Inc(foundCount);
            AddMessage(Format('  (%d,%d): %s', [grid.x, grid.y, EditorID(cellRec)]));
          end;
        end;
      end;

      AddMessage(Format('Found %d cells in area', [foundCount]));
    end;
  end;
end;

// Example 3: Check if cell is at origin
var
  grid: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    grid := GetGridCell(e);

    if (grid.x = 0) and (grid.y = 0) then
      AddMessage(Format('%s is at grid origin (0,0)', [EditorID(e)]))
    else
      AddMessage(Format('%s is at grid (%d,%d)', [EditorID(e), grid.x, grid.y]));
  end;
end;

// Example 4: List cells by distance from origin
var
  childGroup: IwbContainer;
  i, count: integer;
  cellRec: IwbMainRecord;
  grid: TwbGridCell;
  distance: Single;
  cellList: TStringList;
begin
  if Assigned(e) and (Signature(e) = 'WRLD') then begin
    childGroup := ChildGroup(e);
    if Assigned(childGroup) then begin
      cellList := TStringList.Create;
      try
        count := ElementCount(childGroup);
        for i := 0 to count - 1 do begin
          cellRec := ElementByIndex(childGroup, i);
          if Assigned(cellRec) and (Signature(cellRec) = 'CELL') then begin
            grid := GetGridCell(cellRec);
            distance := Sqrt(grid.x*grid.x + grid.y*grid.y);
            cellList.Add(Format('%06.2f: (%d,%d) %s',
              [distance, grid.x, grid.y, EditorID(cellRec)]));
          end;
        end;

        cellList.Sort;
        AddMessage('Cells sorted by distance from origin:');
        for i := 0 to cellList.Count - 1 do
          AddMessage('  ' + cellList[i]);
      finally
        cellList.Free;
      end;
    end;
  end;
end;
```

## See Also

- [wbBlockFromSubBlock - TwbGridCell](TwbGridCell_wbBlockFromSubBlock.md)
- [wbGridCellToGroupLabel - TwbGridCell](TwbGridCell_wbGridCellToGroupLabel.md)
- [wbIsInGridCell - TwbGridCell_](TwbGridCell_wbIsInGridCell.md)
- [wbPositionToGridCell - TwbGridCell_](TwbGridCell_wbPositionToGridCell.md)
- [wbSubBlockFromGridCell - TwbGridCell](TwbGridCell_wbSubBlockFromGridCell.md)


