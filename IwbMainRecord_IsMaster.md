# IsMaster

## Syntax

```pascal
function IsMaster(ARecord: IwbMainRecord): boolean;
```

## Description

Returns `True` when `ARecord` is a master record and `False` otherwise

If provided an argument of an incompatible type, this function will also return `False`.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check if it is a master record |

## Returns

Returns `True` if the record is a master record, `False` otherwise.

## Example

```pascal
if IsMaster(e) then
	AddMessage(Name(e) + ' is a master record');
```

## See Also

- [Master](IwbMainRecord_Master.md)
- [MasterOrSelf](IwbMainRecord_MasterOrSelf.md)


