# IsPositionChanged

## Syntax

```pascal
function IsPositionChanged(aMainRecord: IwbMainRecord): Boolean;
```

## Description

Checks whether the position data of a reference (REFR) record has been modified compared to its master record. This is useful for detecting if a reference has been moved, rotated, or scaled in an override record.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| aMainRecord | IwbMainRecord | The reference record to check for position changes |

## Returns

Returns True if the position, rotation, or scale has changed from the master record, False otherwise.

## Example

```pascal
var
  refRecord: IwbMainRecord;
begin
  refRecord := RecordByFormID(FileByIndex(1), $00012345);

  if IsPositionChanged(refRecord) then
    AddMessage('Reference position has been modified');
end;
```

## See Also

- [wbCopyElementToFile](IwbElement_wbCopyElementToFile.md)
