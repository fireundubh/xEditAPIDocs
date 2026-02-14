# ElementExists

## Syntax

```pascal
function ElementExists(AContainer: IwbContainer; APath: string): boolean;
```

## Description

Checks whether an element exists at the specified path within the container.

This function accesses the ElementExists property, which performs a path lookup without returning the element itself. More efficient than ElementByPath when you only need to check existence. The path uses backslash separators for nested elements. Returns false if any part of the path doesn't exist or for invalid inputs. Useful for conditional logic before accessing potentially missing elements.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to search in |
| APath | string | The element path to check for existence |

## Returns

Returns true if the element exists at the specified path, false otherwise.

## Example

```pascal
begin
  if ElementExists(container, 'Model\MODL') then
    AddMessage('Model path exists');
end;
```

## See Also

- [ElementByPath](IwbContainer_ElementByPath.md)
- [ElementByName](IwbContainer_ElementByName.md)
- [IndexOf](IwbContainer_IndexOf.md)


