# GetFormVCS2

## Syntax

```pascal
function GetFormVCS2(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the native value of the `Version Control Info 2` element

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

- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)
- [SetFormVCS2](IwbMainRecord_SetFormVCS2.md)


