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

- [ChangeFormSignature - IwbMainRecord](IwbMainRecord_ChangeFormSignature.md)
- [ElementBySignature - IwbContainer](IwbContainer_ElementBySignature.md)
- [GroupBySignature - IwbContainer](IwbContainer_GroupBySignature.md)
