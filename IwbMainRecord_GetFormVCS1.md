# GetFormVCS1

## Syntax

```pascal
function GetFormVCS1(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the native value of the `Version Control Info 1` element

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the version control info from |

## Returns

Returns the Version Control Info 1 value as a Cardinal.

## Example

```pascal
r := RecordByFormID(fromPlugin, FixedFormID(e), False);

if Assigned(r) then
begin
	SetFormVCS1(e, GetFormVCS1(r));
	SetFormVCS2(e, GetFormVCS2(r));
end;
```

## See Also

- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)
- [SetFormVCS2](IwbMainRecord_SetFormVCS2.md)


