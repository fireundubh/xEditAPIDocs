# MasterOrSelf

## Syntax

```pascal
function MasterOrSelf(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record overridden by `ARecord`, or the overriding record itself

**Note:** Unlike [Master](IwbMainRecord_Master.md), the return value from this function will always be assigned.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The record to get the master or itself from |

## Returns

Returns the master IwbMainRecord if the record is an override, or the record itself if it is the master.

## Example

```pascal
mr := MasterOrSelf(e);
if Equals(e, mr) then
	AddMessage(Name(e) + ' is the master record')
else
	AddMessage(Name(e) + ' is the overriding record');
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [IsMaster](IwbMainRecord_IsMaster.md)
- [WinningOverride](IwbMainRecord_WinningOverride.md)
- [HighestOverrideOrSelf](IwbMainRecord_HighestOverrideOrSelf.md)


