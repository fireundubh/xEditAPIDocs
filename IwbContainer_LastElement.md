# LastElement

## Syntax

```pascal
function LastElement(AContainer: IwbContainer): IwbElement;
```

## Description

Returns the last element in the container, or nil if there are no children.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to get the last element from |

## Returns

Returns the last element as an IwbElement interface, or nil if the container is empty.

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


