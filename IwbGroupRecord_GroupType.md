# GroupType

## Syntax

```pascal
function GroupType(AGroup: IwbGroupRecord): integer;
```

## Description

Returns the group type for `AGroup`

Possible values:

| Value | Name                                              |
|------:|:--------------------------------------------------|
|     0 | Top                                               |
|     1 | World Children                                    |
|     2 | Interior Cell Block                               |
|     3 | Interior Cell Sub-Block                           |
|     4 | Exterior Cell Block                               |
|     5 | Exterior Cell Sub-Block                           |
|     6 | Cell Children                                     |
|     7 | Topic Children                                    |
|     8 | Cell Persistent Children                          |
|     9 | Cell Temporary Children                           |
|    10 | Cell Visible Distant Children<br />Quest Children |

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AGroup | IwbGroupRecord | The group record to get the type from |

## Returns

The group type as an integer from 0 to 10, or -1 if the argument is not a group.

## Example

```pascal
var
  cellGroup, tempGroup: IwbGroupRecord;
  grpType: integer;
begin
  if not Assigned(e) then
    Exit;

  cellGroup := ChildGroup(e);
  if not Assigned(cellGroup) then
    Exit;

  tempGroup := FindChildGroup(cellGroup, 9, e);
  if Assigned(tempGroup) then begin
    grpType := GroupType(tempGroup);
    AddMessage(IntToStr(grpType));
  end;
end;
```

## See Also

- [FindChildGroup](IwbGroupRecord_FindChildGroup.md)
- [GroupLabel](IwbGroupRecord_GroupLabel.md)


