# GetElementValues

## Syntax

```pascal
function GetElementValues(AContainer: IwbContainer; APath: string): string;
```

## Description

Returns the string display value of an element in the container by path. Useful for things like decoded texture hashes and such.

## Parameters

| Name | Type | Description |
|------|------|-------------|
| AContainer | IwbContainer | The container to retrieve the value from |
| APath | string | The element path to the value |

## Returns

Returns the display value as a string.

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


