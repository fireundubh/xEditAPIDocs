# SetFormVCS1

## Syntax

```pascal
procedure SetFormVCS1(ARecord: IwbMainRecord; AValue: Cardinal);
```

## Description

Changes the native value of the `VCS1` property of `ARecord` to `AValue`

The `VCS1` property corresponds to the `Version Control Info 1` element in the Record Header.

## Example

```pascal
r := RecordByFormID(fromPlugin, FixedFormID(e), False);
if Assigned(r) then
	SetFormVCS1(e, GetFormVCS1(r));
```

## See Also

- [GetFormVCS1 - IwbMainRecord](IwbMainRecord_GetFormVCS1.md)
- [GetFormVCS2 - IwbMainRecord](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS2 - IwbMainRecord](IwbMainRecord_SetFormVCS2.md)
