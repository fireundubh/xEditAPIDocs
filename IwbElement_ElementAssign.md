# ElementAssign

## Syntax

```pascal
function ElementAssign(AContainer: IwbContainer; AIndex: integer; ASource: IwbElement; AOnlySK: boolean): IwbElement;
```

## Description

Copies or creates elements within a container element.

Returns the newly created or copied element.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The destination container element |
| AIndex | integer | The position index where to place the new element (use HighInteger to append, LowInteger or negative for non-arrays) |
| ASource | IwbElement | The source element to copy from (can be nil to create blank element) |
| AOnlySK | boolean | Sorted Key Only flag (use false for normal operations) |

## Returns

Returns the newly created or copied element as an IwbElement interface.

## Example

```pascal
var
  newElement: IwbElement;
begin
  // Append a copy of sourceElement to container
  newElement := ElementAssign(container, HighInteger, sourceElement, False);
end;
```

## See Also

- [IsEditable](IwbElement_IsEditable.md)


