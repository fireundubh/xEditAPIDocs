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

Returns the group type as an integer value (0-10).

## Example

```pascal
var
    childGroup: IwbGroupRecord;
    groupType: integer;
begin
    childGroup := FindChildGroup(ChildGroup(cell), 9, cell);
    groupType  := GroupType(child);

    AddMessage(IntToStr(groupType));  // Output: 9
end;
```

## See Also

- [FindChildGroup](IwbGroupRecord_FindChildGroup.md)
- [GroupLabel](IwbGroupRecord_GroupLabel.md)


