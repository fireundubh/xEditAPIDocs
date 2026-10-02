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

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AGroup | IwbGroupRecord | The child group to get the parent main record from |

## Returns

Returns the parent IwbMainRecord associated with the child group, or nil if not applicable.

## Example

```pascal
var
  grp: IwbGroupRecord;
  owner: IwbMainRecord;
begin
  if not Assigned(e) then
    Exit;

  grp := ChildGroup(e);
  if not Assigned(grp) then
    Exit;

  owner := ChildrenOf(grp);
  if Assigned(owner) then
    AddMessage(Name(owner));
end;
```

## See Also

- [ChildGroup](IwbMainRecord_ChildGroup.md)
- [FindChildGroup](IwbGroupRecord_FindChildGroup.md)


