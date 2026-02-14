# RecordByFormID

## Syntax

```pascal
function RecordByFormID(AFile: IwbFile; AFormID: Integer; AAllowInjected: Boolean): IwbMainRecord;
```

## Description

Returns a record, whose Form ID matches `AFormID`, from `AFile`

If `AAllowInjected` is `True`, **RecordByFormID** will also match against injected records.

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


