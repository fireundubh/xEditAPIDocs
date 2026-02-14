# ElementTypeAsText

## Syntax

```pascal
function ElementTypeAsText(AElement: IwbElement): String;
```

## Description

Returns the element type of `AElement` as a string.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to get the element type from |

## Returns

Returns the element type as a string.

## Example

```pascal
AddMessage(ElementTypeAsText(e));
```

## See Also

- [ElementType](IwbElement_ElementType.md)
- [DefTypeAsText](IwbElement_DefTypeAsText.md)
