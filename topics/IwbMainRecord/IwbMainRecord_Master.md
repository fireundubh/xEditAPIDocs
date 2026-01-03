# Master

## Syntax

```pascal
function Master(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record overridden by `ARecord`, or `Nil` otherwise

## Example

```pascal
mr := Master(e);
if not Assigned(mr) then
	AddMessage(Name(e) + ' is not an overriding record');
```

## See Also

- [IsMaster](IwbMainRecord_IsMaster.md)
- [IsWinningOverride](IwbMainRecord_IsWinningOverride.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)
