# DefTypeAsText

## Syntax

```pascal
function DefTypeAsText(AElement: IwbElement): String;
```

## Description

Returns the definition type of `AElement` as a string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the definition type from |

## Returns

Returns the definition type as a string.

## Example

```pascal
AddMessage(DefTypeAsText(e));
```

## See Also

- [DefType](IwbElement_DefType.md)
- [ElementTypeAsText](IwbElement_ElementTypeAsText.md)
