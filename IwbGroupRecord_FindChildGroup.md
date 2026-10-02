# FindChildGroup

## Syntax

```pascal
function FindChildGroup(AGroup: IwbGroupRecord; AType: integer; AMainRecord: IwbMainRecord): IwbGroupRecord;
```

## Description

Finds and returns a specific child group within another group record.

The search looks at direct children only. A child matches when its group type equals `AType` and its group label equals the FormID of `AMainRecord`. `AType` is the same integer [GroupType](IwbGroupRecord_GroupType.md) uses. Returns nil if either argument is the wrong kind of element, if `AMainRecord` is not assigned, or if no child matches. There is no overload that takes a raw label.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AGroup | IwbGroupRecord | The parent group to search within |
| AType | integer | The group type to search for |
| AMainRecord | IwbMainRecord | The main record associated with the child group |

## Returns

Returns the matching IwbGroupRecord, or nil if no matching group is found.

## Example

```pascal
var
  cellGroup, tempGroup: IwbGroupRecord;
begin
  if not Assigned(e) then
    Exit;

  // e is a CELL. Type 9 is that cell's temporary children.
  cellGroup := ChildGroup(e);
  if not Assigned(cellGroup) then
    Exit;

  tempGroup := FindChildGroup(cellGroup, 9, e);
  if Assigned(tempGroup) then
    AddMessage('Found temporary children');
end;
```

## See Also

- [ChildrenOf](IwbGroupRecord_ChildrenOf.md)
- [GroupLabel](IwbGroupRecord_GroupLabel.md)
- [GroupType](IwbGroupRecord_GroupType.md)


