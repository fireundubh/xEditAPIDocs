# GroupLabel

## Syntax

```pascal
function GroupLabel(aeGroup: IwbGroupRecord): cardinal;
```

## Description

Returns the raw group label value for a group record.

The function retrieves the group label as specified in the file format, returned as a cardinal (32-bit unsigned integer) value. The label's meaning depends on the group type.

## Example

```pascal
var
    group: IwbGroupRecord;
    label: cardinal;
begin
    group := // ... get group reference
    label := GroupLabel(group);
    WriteLn('Group label: ', label);
end;
```

## See Also

- [GroupType](IwbGroupRecord_GroupType.md)


