# ElementAssign

## Syntax

```pascal
function ElementAssign(AContainer: IwbContainer; AIndex: integer; ASource: IwbElement; AOnlySK: boolean): IwbElement;
```

## Description

Copies or creates elements within a container element.

Parameters:
- `AContainer`: Destination container element
- `AIndex`: Position index where to place the new element
  - Use `HighInteger` to append
  - Use `LowInteger` or negative value for non-arrays
- `ASource`: Source element to copy from (can be nil to create blank element)
- `AOnlySK`: Sorted Key Only flag (use False for normal operations)

Returns the newly created or copied element.

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


