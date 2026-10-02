# GroupLabel

## Syntax

```pascal
function GroupLabel(AGroup: IwbGroupRecord): cardinal;
```

## Description

Returns the raw group label value for a group record.

The label's meaning depends on the group type. A top group stores a signature. Cell and topic child groups store a FormID. An interior cell block stores a block number. An exterior cell block stores a packed grid. If the argument is not a group, the result is -1.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AGroup | IwbGroupRecord | The group record to get the label from |

## Returns

The group label as a cardinal, or -1 if the argument is not a group.

## Example

```pascal
var
  grp: IwbGroupRecord;
  grpLabel: cardinal;
begin
  if not Assigned(e) then
    Exit;

  grp := ChildGroup(e);
  if not Assigned(grp) then
    Exit;

  grpLabel := GroupLabel(grp);
  AddMessage('Group label: ' + IntToStr(grpLabel));
end;
```

## See Also

- [GroupType](IwbGroupRecord_GroupType.md)


