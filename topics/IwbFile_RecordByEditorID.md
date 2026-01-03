# RecordByEditorID

## Syntax

```pascal
function RecordByEditorID(AFile: IwbFile; AEditorID: String): IwbMainRecord;
```

## Description

Returns the record, whose Editor ID matches `AEditorID`, from `AFile`

## Examples

```pascal
f := FileByName('Skyrim.esm');
r := RecordByEditorID(f, 'ActionIdle');  // --> ActionIdle [AACT:00013002]
```

## See Also

- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)
- [RecordCount](IwbFile_RecordCount.md)


