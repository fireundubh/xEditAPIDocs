# ElementExists

## Syntax

```pascal
function ElementExists(AContainer: IwbContainer; APath: string): boolean;
```

## Description

Returns whether an element at the specified path exists in the container.

## Examples

```pascal
begin
  if ElementExists(container, 'Model\MODL') then
    AddMessage('Model path exists');
end;
```

## See Also

- [ElementByPath](IwbContainer_ElementByPath.md)
