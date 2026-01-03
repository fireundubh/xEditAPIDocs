# GetFormVersion

## Syntax

```pascal
function GetFormVersion(ARecord: IwbMainRecord): Cardinal;
```

## Description

Return the native value of the Form Version element from the Record Header of `ARecord`


## Example

```pascal
ver := GetFormVersion(e);
  
if ver >= 40 then
	AddMessage(Format('Found form version %d on %s', [ver, Name(e)]));
```

## See Also

- [SetFormVersion](IwbMainRecord_SetFormVersion.md)


