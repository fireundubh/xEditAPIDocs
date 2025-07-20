# BaseRecord

## Syntax

```pascal
function BaseRecord(AReference: IwbMainRecord): IwbMainRecord;
```

## Description

Returns the main record linked to the `NAME` subrecord for `AReference`

**Note:** `AReference` must be a main record with the signature `ACHR` (Placed NPC) or `REFR` (Placed Object).

## Example

```pascal
if Signature(e) <> 'REFR' then
  Exit;

if Signature(BaseRecord(e)) <> 'DOOR' then
  Exit;
```

## See Also

- [BaseRecordID - IwbMainRecord](IwbMainRecord_BaseRecordID.md)
