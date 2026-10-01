# RecordByHexFormID

## Syntax

```pascal
function RecordByHexFormID(AHexFormID: string): IwbMainRecord;
```

## Description

Finds the record in the plugin that owns a load-order FormID.

`AHexFormID` is a hex FormID without a `$` prefix, such as `00000E3A`. A non-string argument raises an invalid-argument error.

The prefix selects one loaded file: the file whose load-order slot equals that prefix. [RecordByFormID](IwbFile_RecordByFormID.md) is then called on that file with the same FormID. The result is the record stored in the owning file, not an override in a later plugin. When the prefix matches no file, or that file has no such record, the result is null.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AHexFormID | string | Load-order FormID as hex, without `$` |

## Returns

The `IwbMainRecord` in the owning file, or null if that file does not contain it.

## Example

```pascal
var
  rec: IwbMainRecord;
begin
  rec := RecordByHexFormID('00000E3A');
  if Assigned(rec) then
    AddMessage(Name(rec));
end;
```

## See Also

- [FileByLoadOrder](Global_FileByLoadOrder.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [RecordByFormID](IwbFile_RecordByFormID.md)
