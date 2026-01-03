# Signature

## Syntax

```pascal
function Signature(ARecord: IwbMainRecord): string;
```

## Description

Returns the signature of `ARecord` (e.g., `ARMA`, `NPC_`, `WEAP`)

## Example

```pascal
if ContainsStr('ACHR REFR', Signature(e)) then
	AddMessage(Name(e) + ' is a reference');
```

## See Also

- [ChangeFormSignature](IwbMainRecord_ChangeFormSignature.md)
- [ElementBySignature](IwbContainer_ElementBySignature.md)
- [GroupBySignature](IwbFile_GroupBySignature.md)


