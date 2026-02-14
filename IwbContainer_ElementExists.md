# ElementExists

## Syntax

```pascal
function ElementExists(AContainer: IwbContainer; APath: string): boolean;
```

## Description

Returns whether an element at the specified path exists in the container.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| APath | string | The element path to check for existence |

## Returns

Returns true if the element exists at the specified path, false otherwise.

## Examples

```pascal
begin
  if ElementExists(container, 'Model\MODL') then
    AddMessage('Model path exists');
end;
```

## See Also

- [ElementByPath](IwbContainer_ElementByPath.md)


