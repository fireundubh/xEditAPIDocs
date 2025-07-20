# RemoveElement

## Syntax

```pascal
function RemoveElement(AContainer: IwbContainer; AChild: Variant): IwbElement;
```

## Description

Removes and returns the specified element from the container.

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
