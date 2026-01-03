# FixedFormID

## Syntax

```pascal
function FixedFormID(ARecord: IwbMainRecord): Cardinal;
```

## Description

Returns the File Form IDof `ARecord`, clamping the Mod ID to the number of master files for the containing file

Local records will not have a load order prefix (e.g., `0x00FFFFFF`) and overrides will have a prefix relative to the record's file's masters.

This function can be used in the resolution of HITME issues.

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

- [FileFormIDtoLoadOrderFormID](../IwbFile/IwbFile_FileFormIDtoLoadOrderFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
