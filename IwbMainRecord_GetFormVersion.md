# GetFormVersion

## Syntax

```pascal
function GetFormVersion(ARecord: IwbMainRecord): Cardinal;
```

## Description

Return the native value of the Form Version element from the Record Header of `ARecord`

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the form version from |

## Returns

Returns the form version as a Cardinal value.

## Example

```pascal
ver := GetFormVersion(e);
  
if ver >= 40 then
	AddMessage(Format('Found form version %d on %s', [ver, Name(e)]));
```

## See Also

- [SetFormVersion](IwbMainRecord_SetFormVersion.md)


