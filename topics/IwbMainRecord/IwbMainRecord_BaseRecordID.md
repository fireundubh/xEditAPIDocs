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

- [BaseRecord - IwbMainRecord](IwbMainRecord_BaseRecord.md)
- [FixedFormID - IwbMainRecord](IwbMainRecord_FixedFormID.md)
- [FormID - IwbMainRecord](IwbMainRecord_FormID.md)
- [GetLoadOrderFormID - IwbMainRecord](IwbMainRecord_GetLoadOrderFormID.md)
- [SetLoadOrderFormID - IwbMainRecord](IwbMainRecord_SetLoadOrderFormID.md)
