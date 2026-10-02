# wbSubBlockFromGridCell

## Syntax

```pascal
function wbSubBlockFromGridCell(GridCell: TwbGridCell): TwbGridCell;
```

## Description

Converts an exterior cell grid coordinate to the sub-block grid coordinate that contains it.

Each sub-block axis is the cell axis divided by 8, and a negative coordinate that is not an exact multiple is rounded toward negative infinity. A sub-block is coarser than a cell and finer than a block. Exterior cell groups in the plugin use this coordinate as the sub-block. Pass the result to `wbBlockFromSubBlock` to get the parent block.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The grid cell coordinate to convert |

## Returns

Returns a TwbGridCell representing the sub-block coordinate.

## Example

```pascal
var
  Cell, SubBlock, Block: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    Cell := GetGridCell(e);
    SubBlock := wbSubBlockFromGridCell(Cell);
    Block := wbBlockFromSubBlock(SubBlock);

    AddMessage(Format('Grid cell [%d, %d]', [Cell.x, Cell.y]));
    AddMessage(Format('  Sub-block: [%d, %d]', [SubBlock.x, SubBlock.y]));
    AddMessage(Format('  Block: [%d, %d]', [Block.x, Block.y]));
  end;
end;
```

## See Also

- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
