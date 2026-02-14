# RecordByIndex

## Syntax

```pascal
function RecordByIndex(AFile: IwbFile; AIndex: Integer): IwbMainRecord;
```

## Description

Returns the record at `AIndex` in `AFile`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to retrieve the record from |
| AIndex | Integer | The zero-based index of the record in the file |

## Returns

Returns the IwbMainRecord at the specified index.

## Examples

```pascal
f := FileByName('Skyrim.esm');
r := RecordByIndex(f, 0);   // --> DoorMarker [STAT:00000001]
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordFromFileByFormID](IwbFile_RecordFromFileByFormID.md)
- [RecordCount](IwbFile_RecordCount.md)


