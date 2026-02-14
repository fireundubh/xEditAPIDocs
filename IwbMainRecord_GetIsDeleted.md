# GetIsDeleted

## Syntax

```pascal
function GetIsDeleted(ARecord: IwbMainRecord): boolean;
```

## Description

Checks whether the record has the Deleted flag set in its record header.

This function retrieves the IsDeleted property, which checks a flag bit in the record's header flags field. Deleted records are typically ignored by the game engine but remain in the file for reference tracking. Returns false for invalid records. This is a header flag, distinct from actually removing the record from the file. Commonly used to mark records as removed without breaking references.

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
- [GetIsInitiallyDisabled](IwbMainRecord_GetIsInitiallyDisabled.md)
- [GetIsPersistent](IwbMainRecord_GetIsPersistent.md)
- [GetIsVisibleWhenDistant](IwbMainRecord_GetIsVisibleWhenDistant.md)


