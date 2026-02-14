# RemoveElement

## Syntax

```pascal
function RemoveElement(AContainer: IwbContainer; AChild: Variant): IwbElement;
```

## Description

Removes and returns the specified element from the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to remove the element from |
| AChild | Variant | The element or element name to remove |

## Returns

Returns the removed element as an IwbElement interface.

## Examples

```pascal
var
  removed: IwbElement;
begin
  removed := RemoveElement(container, 'Model');
end;
```

## See Also

- [RemoveByIndex](IwbContainer_RemoveByIndex.md)


