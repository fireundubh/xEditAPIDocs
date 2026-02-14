# RecordCount

## Syntax

```pascal
function RecordCount(AFile: IwbFile): Integer;
```

## Description

Returns the total number of main records contained in the file.

This function retrieves the RecordCount property, which counts all IwbMainRecord instances in the file (excluding groups and file headers). Returns 0 for empty files or invalid inputs. Use with RecordByIndex to iterate through all records in the file. This count includes all record types (WEAP, NPC_, etc.) but not group records.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AFile | IwbFile | The file to count records in |

## Returns

Returns the number of records in the file.

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


