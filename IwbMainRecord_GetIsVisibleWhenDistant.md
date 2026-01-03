# GetIsVisibleWhenDistant

## Syntax

```pascal
function GetIsVisibleWhenDistant(ARecord: IwbMainRecord): boolean;
```

## Description

Returns whether `ARecord` is flagged as Visible When Distant

## Example

```pascal
if GetIsVisibleWhenDistant(e) then
	AddMessage(Name(e) + ' is flagged as Visible When Distant');
```

## See Also

- [SetIsVisibleWhenDistant](IwbMainRecord_SetIsVisibleWhenDistant.md)


