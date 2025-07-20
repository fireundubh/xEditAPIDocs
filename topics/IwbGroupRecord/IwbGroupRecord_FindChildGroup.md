# FindChildGroup

## Syntax

```pascal
function FindChildGroup(AGroup: IwbGroupRecord; AType: integer; AMainRecord: IwbMainRecord): IwbGroupRecord;
```

## Description

Finds and returns a specific child group within another group record.

The function searches for a child group based on its type and associated main record. The aiType parameter should match the group type values defined in the file format specification. Returns nil if no matching group is found.

Warning: Make sure the aiType value matches the expected group type for the given context.

## Example

```pascal
var
  parentGroup, tempGroup: IwbGroupRecord;
  cell: IwbMainRecord;
begin
  // Get temporary group within a CELL
  tempGroup := FindChildGroup(parentGroup, 9, cell);
  if Assigned(tempGroup) then
    AddMessage('Found temporary group');
end;
```

## See Also

- [IwbGroupRecord Interface](IwbGroupRecord.md)
- [Group Types Reference](GroupTypes.md)
