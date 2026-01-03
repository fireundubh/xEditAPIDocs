# BaseRecordID

## Syntax

```pascal
function BaseRecordID(AReference: IwbMainRecord): Cardinal;
```

## Description

Returns the load order Form ID of the main record linked to the `NAME` subrecord for `AReference`

**Note:** `AReference` must be a main record with the signature `ACHR` (Placed NPC) or `REFR` (Placed Object).

## Example

```pascal
if Signature(e) = 'REFR' then
	RefFormID := BaseRecordID(e);
```

## See Also

- [BaseRecord](IwbMainRecord_BaseRecord.md)
- [FixedFormID](IwbMainRecord_FixedFormID.md)
- [FormID](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID](IwbMainRecord_SetLoadOrderFormID.md)


