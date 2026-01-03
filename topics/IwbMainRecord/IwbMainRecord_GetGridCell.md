# GetGridCell

## Syntax

```pascal
function GetGridCell(ARecord: IwbMainRecord): TwbGridCell;
```

## Description

Returns a `TwbGridCell` object containing the `X` and `Y` coordinates for `ARecord` (must be an exterior cell record)

## Example

```pascal
location := GetGridCell(e);
x := location.x;
y := location.y;
```

## See Also

- [wbBlockFromSubBlock - TwbGridCell](../TwbGridCell/TwbGridCell_wbBlockFromSubBlock.md)
- [wbGridCellToGroupLabel - TwbGridCell](../TwbGridCell/TwbGridCell_wbGridCellToGroupLabel.md)
- [wbIsInGridCell - TwbGridCell_](../TwbGridCell/TwbGridCell_wbIsInGridCell.md)
- [wbPositionToGridCell - TwbGridCell_](../TwbGridCell/TwbGridCell_wbPositionToGridCell.md)
- [wbSubBlockFromGridCell - TwbGridCell](../TwbGridCell/TwbGridCell_wbSubBlockFromGridCell.md)
