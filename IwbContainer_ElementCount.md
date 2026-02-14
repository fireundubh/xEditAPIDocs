# ElementCount

## Syntax

```pascal
function ElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns the total number of elements in the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to count elements in |

## Returns

Returns the total number of elements as an integer.

## Examples

```pascal
var
  count: integer;
begin
  count := ElementCount(container);
  AddMessage('Container has ' + IntToStr(count) + ' elements');
end;
```

## See Also

- [AdditionalElementCount](IwbContainer_AdditionalElementCount.md)


