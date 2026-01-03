# LoadOrderFormIDtoFileFormID

## Syntax

```pascal
function LoadOrderFormIDtoFileFormID(AFile: IwbFile; AFormID: Integer): Cardinal;
```

## Description

Converts `AFormID`, relative to the current load order, to a Form ID relative to `AFile`

## Example

```pascal
f := FileByIndex(0);
fid := reader.ReadInteger;
fid := LoadOrderFormIDtoFileFormID(f, fid);
r := RecordByFormID(f, fid, False);
```

## See Also

- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)


