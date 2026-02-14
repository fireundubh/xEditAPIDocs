# wbIsPseudoESLMode

## Syntax

```pascal
function wbIsPseudoESLMode: Boolean;
```

## Description

Returns whether pseudo ESL (Light) mode is enabled.

## Returns

Returns `True` if pseudo ESL mode is enabled, `False` otherwise.

## Example

```pascal
if wbIsPseudoESLMode then
  AddMessage('Pseudo ESL mode is enabled');
```

## See Also

- [wbIsPseudoLightMode](Global_wbIsPseudoLightMode.md)
- [wbIsPseudoSmallMode](Global_wbIsPseudoSmallMode.md)
