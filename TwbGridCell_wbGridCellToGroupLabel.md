# wbGridCellToGroupLabel

## Syntax

```pascal
function wbGridCellToGroupLabel(GridCell: TwbGridCell): Cardinal;
```

## Description

Converts a grid cell coordinate to the Cardinal label stored on an exterior cell group.

Group labels organize exterior CELL records into hierarchical groups. Each grid cell has one label. This function packs Y in the low 16 bits and X in the high 16 bits. A negative X sets bit 31.

This is particularly useful when working with exterior cell groups, as the group label is stored in the GRUP (group) record header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| GridCell | TwbGridCell | The grid cell coordinate to convert |

## Returns

Returns a Cardinal group label for the specified grid cell. A negative X sets bit 31, which does not fit in a signed 32-bit Integer.

## Example

```pascal
var
  Cell: TwbGridCell;
  GroupLabel: Cardinal;
begin
  if Assigned(e) and (Signature(e) = 'CELL') then begin
    Cell := GetGridCell(e);
    GroupLabel := wbGridCellToGroupLabel(Cell);

    AddMessage(Format('Grid cell [%d, %d] has group label: %u',
      [Cell.x, Cell.y, GroupLabel]));
  end;
end;
```

## See Also

- [GetGridCell](IwbMainRecord_GetGridCell.md)
- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [wbBlockFromSubBlock](TwbGridCell_wbBlockFromSubBlock.md)
