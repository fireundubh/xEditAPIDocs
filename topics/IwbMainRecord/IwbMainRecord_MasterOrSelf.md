# MasterOrSelf

## Syntax

```pascal
function MasterOrSelf(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record overridden by `ARecord`, or the overriding record itself

**Note:** Unlike [Master](IwbMainRecord_Master.md), the return value from this function will always be assigned.

## Example

```pascal
mr := MasterOrSelf(e);
if Equals(e, mr) then
	AddMessage(Name(e) + ' is the master record')
else
	AddMessage(Name(e) + ' is the overriding record');
```

## See Also

- [IsMaster - IwbMainRecord](IwbMainRecord_IsMaster.md)
- [IsWinningOverride - IwbMainRecord](IwbMainRecord_IsWinningOverride.md)
- [Master - IwbMainRecord](IwbMainRecord_Master.md)
