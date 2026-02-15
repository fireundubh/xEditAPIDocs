# wbGridCellToGroupLabel

## Syntax

```pascal
function wbGridCellToGroupLabel(GridCell: TwbGridCell): Integer;
```

## Description

Converts a grid cell coordinate to its corresponding group label integer value.

Group labels are used by the game engine to organize exterior CELL records into hierarchical groups for efficient data management and loading. Each grid cell has a unique integer label that identifies it within the worldspace structure. This function performs the conversion from the two-dimensional grid coordinate (X, Y) to the single integer label used in the plugin file format.

This is particularly useful when working with exterior cell groups, as the group label is stored in the GRUP (group) record header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The grid cell coordinate to convert |

## Returns

Returns an Integer representing the group label for the specified grid cell.

## Example

```pascal
var
  Cell: TwbGridCell;
  GroupLabel: Integer;
begin
  // Get grid cell from an exterior cell record
  Cell := GetGridCell(cellRecord);

  // Convert to group label
  GroupLabel := wbGridCellToGroupLabel(Cell);

  AddMessage(Format('Grid cell [%d, %d] has group label: %d',
    [Cell.x, Cell.y, GroupLabel]));
end;
```

## See Also

- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
