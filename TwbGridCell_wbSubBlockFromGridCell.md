# wbSubBlockFromGridCell

## Syntax

```pascal
function wbSubBlockFromGridCell(GridCell: TwbGridCell): TwbGridCell;
```

## Description

Converts a grid cell coordinate to its corresponding sub-block grid cell coordinate.

In Bethesda's game engines, the worldspace is hierarchically organized into blocks and sub-blocks for efficient LOD (Level of Detail) management and rendering optimization. Sub-blocks are finer subdivisions within the larger block structure. This function calculates the sub-block coordinate for a given grid cell, which is used in LOD generation and distant terrain management.

Sub-blocks are typically used for organizing precombined meshes, distant LOD objects, and optimizing the streaming of world data.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The grid cell coordinate to convert |

## Returns

Returns a TwbGridCell representing the sub-block coordinate.

## Example

```pascal
var
  Cell: TwbGridCell;
  SubBlock: TwbGridCell;
  Block: TwbGridCell;
begin
  // Get grid cell from an exterior cell record
  Cell := GetGridCell(cellRecord);

  // Convert to sub-block coordinate
  SubBlock := wbSubBlockFromGridCell(Cell);

  // Also get parent block for comparison
  Block := wbBlockFromSubBlock(SubBlock);

  AddMessage(Format('Grid cell [%d, %d]', [Cell.x, Cell.y]));
  AddMessage(Format('  Sub-block: [%d, %d]', [SubBlock.x, SubBlock.y]));
  AddMessage(Format('  Block: [%d, %d]', [Block.x, Block.y]));
end;
```

## See Also

- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
