# RecordByFormID

## Syntax

```pascal
function RecordByFormID(AFile: IwbFile; AFormID: Integer; AAllowInjected: Boolean): IwbMainRecord;
```

## Description

Returns a record, whose Form ID matches `AFormID`, from `AFile`

If `AAllowInjected` is `True`, **RecordByFormID** will also match against injected records.

## Example

```pascal
f := FileByName('Skyrim.esm');
r := RecordByFormID(f, $00013002, False);  // --> ActionIdle [AACT:00013002]
```

## See Also

- [RecordByEditorID - IwbFile](IwbFile_RecordByEditorID.md)
- [RecordByIndex - IwbFile](IwbFile_RecordByIndex.md)
- [RecordCount - IwbFile](IwbFile_RecordCount.md)
