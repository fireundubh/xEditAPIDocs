# GetIsVisibleWhenDistant

## Syntax

```pascal
function GetIsVisibleWhenDistant(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Visible When Distant

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to check the Visible When Distant flag on |

## Returns

Returns `True` if the record is flagged as Visible When Distant, `False` otherwise.

## Example

```pascal
if GetIsVisibleWhenDistant(e) then
	AddMessage(Name(e) + ' is flagged as Visible When Distant');
```

## See Also

- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


