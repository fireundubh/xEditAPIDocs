# wbBlockFromSubBlock

## Syntax

```pascal
function wbBlockFromSubBlock(GridCell: TwbGridCell): TwbGridCell;
```

## Description

Converts a sub-block grid cell coordinate to its parent block grid cell coordinate.

In Bethesda's game engines, the worldspace is hierarchically divided into blocks and sub-blocks for efficient data organization and rendering. This function takes a sub-block coordinate and returns the block-level coordinate that contains it. This is useful when working with LOD (Level of Detail) systems and exterior cell organization, where blocks represent larger regions containing multiple sub-blocks.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The sub-block grid cell coordinate to convert |

## Returns

Returns a TwbGridCell representing the parent block coordinate.

## Example

```pascal
var
  SubBlock: TwbGridCell;
  Block: TwbGridCell;
begin
  // Get sub-block from a reference position
  SubBlock := wbPositionToGridCell(GetPosition(refRecord));

  // Convert to parent block coordinate
  Block := wbBlockFromSubBlock(SubBlock);

  AddMessage(Format('Sub-block [%d, %d] is in block [%d, %d]',
    [SubBlock.x, SubBlock.y, Block.x, Block.y]));
end;
```

## See Also

- [wbSubBlockFromGridCell](TwbGridCell_wbSubBlockFromGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
- [GetPosition](IwbMainRecord_GetPosition.md)
