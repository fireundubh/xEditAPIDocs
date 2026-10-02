# wbPositionToGridCell

## Syntax

```pascal
function wbPositionToGridCell(Position: TwbVector): TwbGridCell;
```

## Description

Converts a 3D world position to its corresponding grid cell coordinate.

Grid cells divide the worldspace into squares, 4096 units on a side in the usual games. This function divides the X and Y coordinates by the host cell size and rounds toward negative infinity, including for negative coordinates. Truncation toward zero is not used. The Z coordinate is not used.

This is essential for spatial operations like determining which exterior cell a reference belongs to, organizing objects by location, or validating cell assignments.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Position | TwbVector | The 3D world position to convert |

## Returns

Returns a TwbGridCell containing the X and Y grid coordinates.

## Example

```pascal
var
  RefPos: TwbVector;
  GridCell: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    RefPos := GetPosition(e);
    GridCell := wbPositionToGridCell(RefPos);

    AddMessage(Format('Position (%.2f, %.2f, %.2f) is in grid cell [%d, %d]',
      [RefPos.x, RefPos.y, RefPos.z, GridCell.x, GridCell.y]));
  end;
end;
```

## See Also

- [GetPosition](IwbMainRecord_GetPosition.md)
- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbIsInGridCell](TwbGridCell_wbIsInGridCell.md)
- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
