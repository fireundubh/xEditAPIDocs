# BaseRecord

## Syntax

```pascal
function BaseRecord(AReference: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the main record linked to the `NAME` subrecord for `AReference`

**Note:** `AReference` must be a main record with the signature `ACHR` (Placed NPC) or `REFR` (Placed Object).

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AReference | IwbMainRecord | The reference record (ACHR or REFR) to get the base record from |

## Returns

Returns the IwbMainRecord linked to the NAME subrecord of the reference.

## Example

```pascal
if Signature(e) <> 'REFR' then
  Exit;

if Signature(BaseRecord(e)) <> 'DOOR' then
  Exit;
```

## See Also

- [BaseRecordID](IwbMainRecord_BaseRecordID.md)


