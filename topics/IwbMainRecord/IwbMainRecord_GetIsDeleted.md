# GetIsDeleted

## Syntax

```pascal
function GetIsDeleted(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Deleted

## Example

```pascal
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is flagged as Deleted');
```

## See Also

- [SetIsDeleted](IwbMainRecord_SetIsDeleted.md)
