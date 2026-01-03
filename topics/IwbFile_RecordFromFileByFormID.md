# RecordFromFileByFormID

## Syntax

```pascal
function RecordFromFileByFormID(AFile: IwbFile|string; AFormID: integer|string): IwbMainRecord;
```

## Description

Returns the record, whose Form ID matches `AFormID`, from `AFile`.

`AFile` may be specified as an `IwbFile` or as a filename string. `AFormID` may be specified as an `Integer` or as a hex string.

The module's ID prefix will be corrected internally to accommodate for small or medium flags in files that support it. Leading zeroes in the hex string for `AFormID` are not mandatory.

## Examples

```pascal
var
  eFile : IwbFile;
  rec   : IwbMainRecord;
begin
  eFile := FileByName('Skyrim.esm');
  rec := RecordFromFileByFormID(eFile, $0000000F);
  rec := RecordFromFileByFormID(eFile, '0000000F');
  rec := RecordFromFileByFormID('Skyrim.esm', '0000000F');
end;
```

## See Also

- [RecordByEditorID](IwbFile_RecordByEditorID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
- [RecordByIndex](IwbFile_RecordByIndex.md)


