# ChangeFormSignature

## Syntax

```pascal
procedure ChangeFormSignature(ARecord: IwbMainRecord; ANewSignature: string);
```

## Description

Changes the signature (record type) of a main record to a new value.

The procedure modifies only the 4-character signature of the record while preserving all other record data. This should be used with caution as changing record signatures can break references and functionality if not done correctly.

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

- [Signature - IwbMainRecord](IwbMainRecord_Signature.md)
