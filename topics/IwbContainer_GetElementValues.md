# GetElementValues

## Syntax

```pascal
function GetElementValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the string display value of an element in the container by path. Useful for things like decoded texture hashes and such.

## Examples

```pascal
var
  value: string;
begin
  value := GetElementValues(container, 'Model\MODT\Textures\Texture\File Hash');
end;
```

## See Also

- [GetValue](IwbElement_GetValue.md)


