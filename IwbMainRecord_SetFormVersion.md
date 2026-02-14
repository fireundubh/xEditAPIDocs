# SetFormVersion

## Syntax

```pascal
procedure SetFormVersion(ARecord: IwbMainRecord; AVersion: Cardinal);
```

## Description

Changes the native value of the `Version` property of `ARecord` to `AVersion`

The `Version` property corresponds to the `Form Version` element in the Record Header.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to set the form version on |
| AVersion | Cardinal | The new form version value |

## Example

```pascal
ver := GetFormVersion(e);
if ver >= 40 then
begin
	AddMessage(Format('Found form version %d on %s', [ver, Name(e)]));
	SetFormVersion(e, 43);
end;
```

## See Also

- [GetFormVersion](IwbMainRecord_GetFormVersion.md)


