# ChildrenOf

## Syntax

```pascal
function ChildrenOf(AGroup: IwbGroupRecord): IwbMainRecord;
```

## Description

If `AGroup` is a child group, this function returns the main record that it is associated with.

For example, a Dialogue Topic (`DIAL`) is followed by a group (`GRUP`) that contains its Infos (`INFO`); passing that
`GRUP` to this function would retrieve the `DIAL`.

Similarly, cells (`CELL`) and worldspaces (`WRLD`) have their contents organized in a comparable manner to Dialogue
Topics. As a result, this function will work with them as well, returning their corresponding parent main record.

## Example

```pascal
var
    cell: IwbMainRecord;
begin
    // get CELL record of GRUP record
    cell := ChildrenOf(cell);
    
    if not Assigned(cell) then
        Exit;
    
    // dump reference if matches location type
    if GetElementNativeValues(cell, 'XLCN') = LCTNRef then
        AddMessage(Name(e));
end;
```

## See Also

- [ChildGroup - IwbMainRecord](IwbMainRecord_ChildGroup.md)
- [FindChildGroup - IwbGroupRecord](IwbGroupRecord_FindChildGroup.md)
