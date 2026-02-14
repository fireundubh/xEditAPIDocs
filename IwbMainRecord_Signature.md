# Signature

## Syntax

```pascal
function Signature(ARecord: IwbMainRecord): string;
```

## Description

Returns the 4-character record type signature.

This function retrieves the Signature property, which identifies the record type (e.g., "WEAP" for weapons, "NPC_" for NPCs, "ARMA" for armor addons). The signature determines which definition template the record uses and what fields it contains. Returns an empty string for invalid records. Signatures are always exactly 4 characters, padded with underscores if needed.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| ARecord | IwbMainRecord | The main record to get the signature from |

## Returns

Returns the 4-character signature of the record as a string.

## Example

```pascal
if ContainsStr('ACHR REFR', Signature(e)) then
	AddMessage(Name(e) + ' is a reference');
```

## See Also

- [ChangeFormSignature](IwbMainRecord_ChangeFormSignature.md)
- [EditorID](IwbMainRecord_EditorID.md)
- [FormID](IwbMainRecord_FormID.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)


