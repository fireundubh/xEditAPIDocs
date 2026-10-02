# wbBlockFromSubBlock

## Syntax

```pascal
function wbBlockFromSubBlock(GridCell: TwbGridCell): TwbGridCell;
```

## Description

Converts a sub-block grid coordinate to the block grid coordinate that contains it.

The argument must already be a sub-block, such as the result of `wbSubBlockFromGridCell`. A cell from `wbPositionToGridCell` or `GetGridCell` is not a sub-block. Each block axis is that sub-block axis divided by 4, and a negative coordinate that is not an exact multiple is rounded toward negative infinity. Exterior cell groups in the plugin use this coarser coordinate as the block.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The sub-block grid cell coordinate to convert |

## Returns

Returns a TwbGridCell representing the parent block coordinate.

## Example

```pascal
var
  RefPos: TwbVector;
  Cell, SubBlock, Block: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    RefPos := GetPosition(e);
    Cell := wbPositionToGridCell(RefPos);
    SubBlock := wbSubBlockFromGridCell(Cell);
    Block := wbBlockFromSubBlock(SubBlock);

    AddMessage(Format('Cell [%d, %d] is in sub-block [%d, %d], block [%d, %d]',
      [Cell.x, Cell.y, SubBlock.x, SubBlock.y, Block.x, Block.y]));
  end;
end;
```

## See Also

- [wbSubBlockFromGridCell](TwbGridCell_wbSubBlockFromGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbGridCellToGroupLabel](TwbGridCell_wbGridCellToGroupLabel.md)
- [GetPosition](IwbMainRecord_GetPosition.md)
