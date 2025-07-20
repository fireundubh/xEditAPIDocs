# IsWinningOverride

## Syntax

```pascal
function IsWinningOverride(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` loads last in the current load order

## Example

```pascal
if IsWinningOverride(e) then
	AddMessage(Name(e) + ' is the winning override');
```

## See Also

- [Master - IwbMainRecord](IwbMainRecord_Master.md)
- [MasterOrSelf - IwbMainRecord](IwbMainRecord_MasterOrSelf.md)
