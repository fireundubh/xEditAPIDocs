# wbIsInGridCell

## Syntax

```pascal
function wbIsInGridCell(Position: TwbVector; GridCell: TwbGridCell): Boolean;
```

## Description

Determines whether a 3D position falls within the boundaries of a specified grid cell.

Grid cells are square regions in the worldspace, typically 4096 units on each side. This function checks if the X and Y coordinates of a position vector fall within the bounds of the given grid cell. The Z coordinate (height) is not considered, as grid cells represent horizontal divisions of the world.

This is useful for spatial queries, such as finding which references or objects are located in a particular grid cell, or validating that reference positions match their parent cell's coordinates.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| Position | TwbVector | The 3D position to test (uses X and Y components only) |
| GridCell | TwbGridCell | The grid cell to test against |

## Returns

Returns `True` if the position is within the grid cell boundaries, `False` otherwise.

## Example

```pascal
var
  RefPos: TwbVector;
  Origin: TwbGridCell;
begin
  if Assigned(e) and (Signature(e) = 'REFR') then begin
    RefPos := GetPosition(e);
    Origin := wbGridCell(0, 0);

    if wbIsInGridCell(RefPos, Origin) then
      AddMessage(Name(e) + ' is inside cell 0, 0');
  end;
end;
```

## See Also

- [wbPositionToGridCell](TwbGridCell_wbPositionToGridCell.md)
- [GetPosition](IwbMainRecord_GetPosition.md)
- [GetGridCell](IwbMainRecord_GetGridCell.md)
