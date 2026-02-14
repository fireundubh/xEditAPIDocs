# Signature

## Syntax

```pascal
function Signature(ARecord: IwbMainRecord): string;
```

## Description

Returns the signature of `ARecord` (e.g., `ARMA`, `NPC_`, `WEAP`)

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
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)


