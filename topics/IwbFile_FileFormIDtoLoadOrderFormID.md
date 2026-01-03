# FileFormIDtoLoadOrderFormID

## Syntax

```pascal
function FileFormIDtoLoadOrderFormID(AFile: IwbFile; AFormID: Integer): Cardinal;
```

## Description

Converts `AFormID`, relative to `AFile`, to a Form ID relative to the current load order

## Example

```pascal
fid := FixedFormID(e);
fid := FileFormIDtoLoadOrderFormID(f, fid);
rec := RecordByFormID(f, fid, True);
```

## See Also

- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)


