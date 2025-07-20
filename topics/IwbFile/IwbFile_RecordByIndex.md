# RecordByIndex

## Syntax

```pascal
function RecordByIndex(AFile: IwbFile; AIndex: Integer): IwbMainRecord;
```

## Description

Returns the record at `AIndex` in `AFile`

## Examples

```pascal
f := FileByName('Skyrim.esm');
r := RecordByIndex(f, 0);   // --> DoorMarker [STAT:00000001]
```

## See Also

- [RecordByEditorID - IwbFile](IwbFile_RecordByEditorID.md)
- [RecordByFormID - IwbFile](IwbFile_RecordByFormID.md)
- [RecordCount - IwbFile](IwbFile_RecordCount.md)
