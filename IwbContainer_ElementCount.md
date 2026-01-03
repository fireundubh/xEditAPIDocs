# ElementCount

## Syntax

```pascal
function ElementCount(AContainer: IwbContainer): integer;
```

## Description

Returns the total number of elements in the container.

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


