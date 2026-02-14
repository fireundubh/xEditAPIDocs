# SetToDefault

## Syntax

```pascal
procedure SetToDefault(AElement: IwbElement);
```

## Description

Resets the element to its default value and ensures required substructures exist.

This function calls the element's SetToDefault method, which restores the element's data to the default value specified in its definition and creates any missing required child elements. Useful for initializing new records or resetting corrupted data. The exact behavior depends on the element type: simple values reset to their default, containers ensure required children exist. The element must be editable.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AElement | IwbElement | The element to reset to default |

## Example

```pascal
var
    element: IwbElement;
begin
    SetToDefault(element);
end;
```

## See Also

- [Check](IwbElement_Check.md)


