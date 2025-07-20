# LastElement

## Syntax

```pascal
function LastElement(AContainer: IwbContainer): IwbElement;
```

## Description

Returns the last element in the container, or nil if there are no children.

## Examples

```pascal
var
  last: IwbElement;
begin
  last := LastElement(container);
end;
```

## See Also

- [ElementByIndex](IwbContainer_ElementByIndex.md)
- [ElementCount](IwbContainer_ElementCount.md)
