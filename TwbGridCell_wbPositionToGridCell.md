# wbPositionToGridCell

## Syntax

```pascal
function wbPositionToGridCell(Position: TwbVector): TwbGridCell;
```

## Description

Converts a 3D world position to its corresponding grid cell coordinate.

Grid cells divide the game's worldspace into a grid of square regions, typically 4096 units on each side. This function calculates which grid cell contains the given position by dividing the X and Y coordinates by the grid cell size and rounding down. The Z coordinate (height) is not used in the calculation, as grid cells represent horizontal divisions of the world.

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
  // Get position from a reference record
  RefPos := GetPosition(refRecord);

  // Convert to grid cell coordinates
  GridCell := wbPositionToGridCell(RefPos);

  AddMessage(Format('Position (%.2f, %.2f, %.2f) is in grid cell [%d, %d]',
    [RefPos.x, RefPos.y, RefPos.z, GridCell.x, GridCell.y]));
end;
```

## See Also

- [GetPosition](IwbMainRecord_GetPosition.md)
- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbIsInGridCell](TwbGridCell_wbIsInGridCell.md)
- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
