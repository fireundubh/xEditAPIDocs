# RecordByEditorID

## Syntax

```pascal
function RecordByEditorID(AFile: IwbFile; AEditorID: String): IwbMainRecord;
```

## Description

Searches the file for a main record with the specified Editor ID.

This function accesses the RecordByEditorID property, which performs a case-sensitive lookup for records with matching EDID values. Only searches within the specified file, not in masters or other plugins. Returns nil if no record with that Editor ID exists in the file. More efficient than iterating through all records manually.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search for the record |
| AEditorID | String | The Editor ID of the record to find |

## Returns

Returns the IwbMainRecord with the matching Editor ID, or nil if not found.

## Example

```pascal
f := FileByName('Skyrim.esm');
r := RecordByEditorID(f, 'ActionIdle');  // --> ActionIdle [AACT:00013002]
```

## See Also

- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [RecordCount](IwbFile_RecordCount.md)


