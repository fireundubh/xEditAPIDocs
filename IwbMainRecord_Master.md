# Master

## Syntax

```pascal
function Master(ARecord: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the master record overridden by `ARecord`, or `Nil` otherwise

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The overriding record to get the master from |

## Returns

Returns the master IwbMainRecord that is overridden, or Nil if the record is not an override.

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


