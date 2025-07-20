# MainRecordByEditorID

## Syntax

```pascal
function MainRecordByEditorID(AGroup: IwbGroupRecord; AEditorID: string): IwbMainRecord;
```

## Description

Searches for a main record within a group by its Editor ID.

The function performs a search through the specified group to find a main record matching the given Editor ID. Returns nil if no matching record is found.

Note: This function is not optimized for performance and should be used sparingly, especially with large groups.

## Example

```pascal
var
    group: IwbGroupRecord;
    record: IwbMainRecord;
begin
    group := // ... get group reference
    record := MainRecordByEditorID(group, 'ArmorIronHelmet');
    if Assigned(record) then
        AddMessage('Found record: ' + EditorID(record));
end;
```

## See Also

- [EditorID - IwbMainRecord](IwbMainRecord_EditorID.md)
- [RecordByEditorID - IwbFile](IwbFile_RecordByEditorID.md)
