# IsWinningOverride

## Syntax

```pascal
function IsWinningOverride(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` loads last in the current load order

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check if it is the winning override |

## Returns

Returns `True` if the record loads last in the current load order, `False` otherwise.

## Example

```pascal
if IsWinningOverride(e) then
	AddMessage(Name(e) + ' is the winning override');
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)


