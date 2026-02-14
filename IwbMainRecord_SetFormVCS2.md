# SetFormVCS2

## Syntax

```pascal
procedure SetFormVCS2(ARecord: IwbMainRecord; AValue: Cardinal);
```

## Description

Changes the native value of the `VCS2` property of `ARecord` to `AValue`

The `VCS2` property corresponds to the `Version Control Info 2` element in the Record Header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the version control info on |
| AValue | Cardinal | The new Version Control Info 2 value |

## Example

```pascal
r := RecordByFormID(fromPlugin, FixedFormID(e), False);
if Assigned(r) then
	SetFormVCS2(e, GetFormVCS2(r));
```

## See Also

- [GetFormVCS1](IwbMainRecord_GetFormVCS1.md)
- [GetFormVCS2](IwbMainRecord_GetFormVCS2.md)
- [SetFormVCS1](IwbMainRecord_SetFormVCS1.md)


