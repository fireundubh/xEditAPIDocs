# RecordCount

## Syntax

```pascal
function RecordCount(AFile: IwbFile): Integer;
```

## Description

Returns the number of records in `AFile`

## Example

```pascal
f := FileByName('Skyrim.esm');
for i := 0 to Pred(RecordCount(f)) do
	r := RecordByIndex(f, i);  // IwbMainRecord
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)


