# RecordByFormID

## Syntax

```pascal
function RecordByFormID(AFile: IwbFile; AFormID: Integer; AAllowInjected: Boolean): IwbMainRecord;
```

## Description

Searches the file for a main record with the specified FormID.

This function accesses the RecordByFormID property, which performs a lookup for records matching the provided FormID. The FormID should be in load order format. The AAllowInjected parameter controls whether injected records (records added programmatically, not from disk) are included in the search. Returns nil if no matching record is found. Always performs full FormID resolution.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to search for the record |
| AFormID | Integer | The Form ID of the record to find |
| AAllowInjected | Boolean | Whether to include injected records in the search |

## Returns

Returns the IwbMainRecord with the matching Form ID, or nil if not found.

## Example

```pascal
f := FileByName('Skyrim.esm');
r := RecordByFormID(f, $00013002, False);  // --> ActionIdle [AACT:00013002]
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [RecordCount](IwbFile_RecordCount.md)


