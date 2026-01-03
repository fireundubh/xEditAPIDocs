# IsMaster

## Syntax

```pascal
function IsMaster(ARecord: IwbMainRecord): boolean;
```

## Description

Returns `True` when `ARecord` is a master record and `False` otherwise

If provided an argument of an incompatible type, this function will also return `False`.

## Example

```pascal
if IsMaster(e) then
	AddMessage(Name(e) + ' is a master record');
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)


