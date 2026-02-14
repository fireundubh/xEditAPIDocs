# SetIsDeleted

## Syntax

```pascal
procedure SetIsDeleted(ARecord: IwbMainRecord; AFlag: boolean);
```

## Description

Sets or clears the Deleted flag in the record's header.

This function assigns to the IsDeleted property, which modifies a flag bit in the record header. Setting this to true marks the record as deleted (ignored by the game but preserved for reference tracking). Setting to false undeletes the record. The change takes effect immediately in memory but must be saved to persist. Prefer this over Remove when you want to preserve the record structure for dependency tracking.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the Deleted flag on |
| AFlag | boolean | Whether to set (True) or clear (False) the Deleted flag |

## Example

```pascal
SetIsDeleted(e, True);
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is flagged as Deleted');
  
SetIsDeleted(e, False);
if GetIsDeleted(e) then
	AddMessage(Name(e) + ' is not flagged as Deleted');
```

## See Also

- [GetIsDeleted](IwbMainRecord_GetIsDeleted.md)
- [SetIsInitiallyDisabled](IwbMainRecord_SetIsInitiallyDisabled.md)
- [SetIsPersistent](IwbMainRecord_SetIsPersistent.md)
- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


