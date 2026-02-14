# ChangeFormSignature

## Syntax

```pascal
procedure ChangeFormSignature(ARecord: IwbMainRecord; ANewSignature: string);
```

## Description

Changes the signature (record type) of a main record to a new value.

The procedure modifies only the 4-character signature of the record while preserving all other record data. This should be used with caution as changing record signatures can break references and functionality if not done correctly.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to change the signature of |
| ANewSignature | string | The new 4-character signature to assign to the record |

## Example

```pascal
var
    record: IwbMainRecord;
begin
    record := // ... get record reference
    ChangeFormSignature(record, 'ARMO'); // Changes record signature to ARMO
end;
```

## See Also

- [Signature](IwbMainRecord_Signature.md)
- [FormID](IwbMainRecord_FormID.md)
- [EditorID](IwbMainRecord_EditorID.md)


