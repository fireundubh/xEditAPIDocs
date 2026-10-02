# MainRecordByEditorID

## Syntax

```pascal
function MainRecordByEditorID(AGroup: IwbGroupRecord; AEditorID: string): IwbMainRecord;
```

## Description

Searches for a main record within a group by its Editor ID.

Only direct children that are main records are examined. Nested groups are not opened. The Editor ID comparison is case-insensitive. Returns nil if nothing matches or the argument is not a group. The scan is linear, so it is a poor choice for a large top-level group.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AGroup | IwbGroupRecord | The group to search within |
| AEditorID | string | The Editor ID of the record to find |

## Returns

Returns the IwbMainRecord with the matching Editor ID, or nil if not found.

## Example

```pascal
var
  armors: IwbGroupRecord;
  rec: IwbMainRecord;
begin
  if not Assigned(e) then
    Exit;

  armors := GroupBySignature(GetFile(e), 'ARMO');
  if not Assigned(armors) then
    Exit;

  rec := MainRecordByEditorID(armors, 'ArmorIronHelmet');
  if Assigned(rec) then
    AddMessage('Found record: ' + EditorID(rec));
end;
```

## See Also

- [EditorID](IwbMainRecord_EditorID.md)
- [RecordByEditorID](IwbFile_RecordByEditorID.md)


