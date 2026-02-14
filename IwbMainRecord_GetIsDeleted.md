# GetIsDeleted

## Syntax

```pascal
function GetIsDeleted(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Deleted

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Deleted flag on |

## Returns

Returns `True` if the record is flagged as Deleted, `False` otherwise.

## Example

```pascal
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is flagged as Deleted');
```

## See Also

- [SetIsDeleted](IwbMainRecord_SetIsDeleted.md)


