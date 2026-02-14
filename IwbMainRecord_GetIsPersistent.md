# GetIsPersistent

## Syntax

```pascal
function GetIsPersistent(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Persistent

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Persistent flag on |

## Returns

Returns `True` if the record is flagged as Persistent, `False` otherwise.

## Example

```pascal
if GetIsPersistent(e) then
	AddMessage(Name(e) + ' is flagged as Persistent');
```

## See Also

- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)


